---
title: SQL 数据库的 XEvent 环形缓冲区代码 | Microsoft 文档
description: 提供一个 Transact-SQL 代码示例，以帮助你快速轻松地在 Azure SQL 数据库中使用环形缓冲区目标。
services: sql-database
ms.service: sql-database
ms.subservice: monitor
ms.custom: ''
ms.devlang: PowerShell
ms.topic: conceptual
author: MightyPen
ms.author: genemi
ms.reviewer: jrasnik
manager: craigg
ms.date: 12/19/2018
ms.openlocfilehash: f47c6b63ce5f18aa896b086ec884b9a3020cadd2
ms.sourcegitcommit: 2d0fb4f3fc8086d61e2d8e506d5c2b930ba525a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2019
ms.locfileid: "57993279"
---
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a>SQL 数据库中扩展事件的环形缓冲区目标代码

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

需要完整的代码示例以最简单快速的方式在测试期间捕获和报告扩展事件的信息。 扩展事件数据最简单的目标是[环形缓冲区目标](https://msdn.microsoft.com/library/ff878182.aspx)。

本主题演示一个 Transact-SQL 代码示例：

1. 创建一个包含要演示的数据的表。
2. 创建现有扩展事件的会话，即 **sqlserver.sql_statement_starting**。
   
   * 此事件仅限于包含特定 Update 字符串的 SQL 语句：**statement LIKE '%UPDATE tabEmployee%'**。
   * 选择要将事件的输出发送给环形缓冲区类型的目标，即 **package0.ring_buffer**。
3. 启动事件会话。
4. 发出几个简单的 SQL UPDATE 语句。
5. 发出 SQL SELECT 语句，从环形缓冲区检索事件输出。
   
   * **sys.dm_xe_database_session_targets** 和其他动态管理视图 (DMV) 联接在一起。
6. 停止事件会话。
7. 删除环形缓冲区目标以释放其资源。
8. 删除事件会话和演示表。

## <a name="prerequisites"></a>必备组件

* Azure 帐户和订阅。 可以注册[免费试用版](https://azure.microsoft.com/pricing/free-trial/)。
* 可以在其中创建表的任何数据库。
  
  * 或者，也可以快速[创建一个 **AdventureWorksLT** 演示数据库](sql-database-get-started.md)。
* SQL Server Management Studio (ssms.exe)，最好是每月更新版。 
  可从以下位置下载最新的 ssms.exe：
  
  * 标题为[下载 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 的主题。
  * [直接指向下载位置的链接。](https://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a>代码示例

只要稍加修改，就可以在 Azure SQL 数据库或 Microsoft SQL Server 上运行以下环形缓冲区的代码示例。 不同之处在于步骤 5 的 FROM 子句中使用的某些动态管理视图 (DMV) 名称出现了节点“_database”。 例如：

* sys.dm_xe<strong>_database</strong>_session_targets
* sys.dm_xe_session_targets

&nbsp;

```sql
GO
----  Transact-SQL.
---- Step set 1.

SET NOCOUNT ON;
GO


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'tabEmployee')
BEGIN
    DROP TABLE tabEmployee;
END
GO


CREATE TABLE tabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO tabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO

---- Step set 2.


IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'eventsession_gm_azuresqldb51')
BEGIN
    DROP EVENT SESSION eventsession_gm_azuresqldb51
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE '%UPDATE tabEmployee%'
            )
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
GO

---- Step set 3.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = START;
GO

---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
GO

---- Step set 5.


SELECT
    se.name                      AS [session-name],
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source,
    st.target_data,
    CAST(st.target_data AS XML)  AS [target_data_XML]
FROM
               sys.dm_xe_database_session_event_actions  AS ac

    INNER JOIN sys.dm_xe_database_session_events         AS ev  ON ev.event_name = ac.event_name
        AND CAST(ev.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_object_columns AS oc
         ON CAST(oc.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_targets        AS st
         ON CAST(st.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_sessions               AS se
         ON CAST(ac.event_session_address AS BINARY(8)) = CAST(se.address AS BINARY(8))
WHERE
        oc.column_name = 'occurrence_number'
    AND
        se.name        = 'eventsession_gm_azuresqldb51'
    AND
        ac.action_name = 'sql_text'
ORDER BY
    se.name,
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source
;
GO

---- Step set 6.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = STOP;
GO

---- Step set 7.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO

---- Step set 8.


DROP EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE;
GO

DROP TABLE tabEmployee;
GO
```


&nbsp;

## <a name="ring-buffer-contents"></a>环形缓冲区内容

我们使用了 ssms.exe 来运行该代码示例。

为了查看结果，我们单击了 **target_data_XML** 列标题下的单元格。

然后，在结果窗格中，我们单击了 **target_data_XML** 列标题下的单元格。 这个单击动作在 ssms.exe 中按结果单元格内容显示的顺序，以 XML 格式创建了另一个文件选项卡。

输出显示在以下块中。 结果看起来很长，但其实只是两个 **<event>** 元素。

&nbsp;

```
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="1728">
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.317Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>7</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>184</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>328</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.327Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>10</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>340</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>486</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
</RingBufferTarget>
```


#### <a name="release-resources-held-by-your-ring-buffer"></a>释放环形缓冲区占用的资源

处理完环形缓冲区后，可以发出 **ALTER** 将它删除并释放其资源，如下所示：

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


事件会话的定义会更新，但不会删除。 然后可以将环形缓冲区的另一个实例添加到事件会话：

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a>详细信息

有关 Azure SQL 数据库中扩展事件的主要主题是：

* [SQL 数据库中扩展事件的注意事项](sql-database-xevent-db-diff-from-svr.md)，对比 Azure SQL 数据库与 Microsoft SQL Server 的扩展事件的某些方面。

可通过以下链接访问有关扩展事件的其他代码示例主题。 不过，必须定期检查所有示例，以确定这些示例是针对 Microsoft SQL Server 还是 Azure SQL 数据库。 然后，可以在运行示例时确定是否要做出细微的更改。

* Azure SQL 数据库的代码示例：[SQL 数据库中扩展事件的事件文件目标代码](sql-database-xevent-code-event-file.md)

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](https://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find the Objects That Have the Most Locks Taken on Them](https://msdn.microsoft.com/library/bb630355.aspx)
-->
