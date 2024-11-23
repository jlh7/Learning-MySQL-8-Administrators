# 1st day [2024-11-23]

- **Comprehensive overview of MySQL 8**: The chapter provided a thorough introduction to MySQL, its key features, and the significant enhancements introduced in MySQL 8.

- **Benefits and limitations**: It explored the advantages of using MySQL for various applications, while also addressing its limitations to provide a balanced perspective.

- **Real-world use cases**: The chapter showcased compelling examples of how organizations like Facebook, YouTube, and Netflix leverage MySQL to power their services, demonstrating its versatility and scalability.

## [I.What is MySQL?](https://dev.mysql.com/doc/refman/8.0/en/what-is-mysql.html)

- **MySQL is a popular open-source relational database**: Known for its performance, ease of use, and reliability, it's widely used by web applications, including major platforms like Facebook, Twitter, and Wikipedia.

- **MySQL 8 offers significant improvements**: This version is optimized for handling massive datasets and addressing new use cases in the digital age, such as analyzing data from social networks, e-commerce, and banking transactions.

### 1.[What is a Relational Database (RDBMS)?](<What is a Relational Database (RDBMS).md>)

**RDBMS is the foundation**: Relational Database Management Systems (RDBMS) rely on SQL to manage structured data organized in tables with relationships between them.

### 2.What is SQL?

- **SQL is the language for relational databases**: It's used to perform various actions like retrieving, adding, updating, and deleting data in systems like MySQL, Oracle, and MS SQL Server.

- **SQL is versatile and embeddable**: It allows users to define and manipulate data, control access permissions, and can be integrated with other programming languages for enhanced functionality.

### 3.MySQL as a RDBMS

- **Organized data for efficient retrieval**: Relational databases like MySQL store data in tables with rows and columns, allowing for efficient organization and retrieval of information.

- **Relationships between tables**: MySQL enables connections between tables (one-to-many, many-to-one, one-to-one) using primary keys, foreign keys, and indexes, facilitating complex queries and data management.

- **SQL as the interface**: SQL is the standard language used to interact with MySQL, allowing for data creation, deletion, modification, and retrieval.

### 4.License requirements of MySQL is General Public License (GNU)

- **Open source benefits**: MySQL's open-source nature provides flexibility and cost savings, allowing users to customize the source code to fit their specific needs.

- **Freedom under GNU license**: The GNU General Public License allows for free use of MySQL in web applications, studying its code, and modifying it as needed.

- **Enterprise support available**: Despite being open source, MySQL also offers an Enterprise Edition with advanced features and support contracts for businesses that require assistance.

### 5.Reliability and scalability

- **High Reliability**: MySQL is designed for stability and performance, minimizing the need for extensive troubleshooting and performance tuning.

- **Performance Enhancements**: Features like indexing, load utilities, and memory caching contribute to MySQL's efficient data handling.

- **Scalability**: MySQL uses the InnoDB storage engine for [`ACID-compliant`](https://dev.mysql.com/doc/refman/8.0/en/mysql-acid.html) transactions and offers replication and clustering capabilities to handle growing databases.

### 6.Platform compatibility

- **Cross-platform compatibility**: MySQL runs on various operating systems, including Linux distributions (RedHat, Ubuntu), Windows, and macOS, making it widely accessible.

- **API connectivity**: MySQL provides APIs for integration with a wide range of programming languages like C++, Java, Python, and PHP, enabling developers to build diverse applications.

- **Increased popularity**: This cross-platform support and API connectivity contribute to MySQL's widespread adoption across different development environments.

## II.Core features in MySQL

### 1.Structured database

- **Structured databases are organized and predefined**: These databases use a fixed schema with predefined data types and lengths, making them suitable for organized data like financial transactions and inventory management.

- **Unstructured databases handle diverse data**: These databases lack a rigid structure and can store various data types like emails, images, and documents, making them suitable for managing less organized information.

- **Different strengths for different needs**: Structured databases excel in efficient querying and analysis of organized data, while unstructured databases offer flexibility for managing diverse data types.

### 2.[Database storage engines and types](https://dev.mysql.com/doc/refman/8.0/en/storage-engines.html)

#### 2.1.Engines

- **Storage engines determine data handling**: MySQL uses different storage engines to manage how data is stored and accessed in tables. Each engine has unique characteristics affecting performance and functionality.

- **InnoDB is the default**: In MySQL 8, InnoDB is the default storage engine, known for its reliability, transaction support, and [`ACID-compliant`](https://dev.mysql.com/doc/refman/8.0/en/mysql-acid.html).

- **MySQL allows for flexibility**: MySQL's architecture allows users to load and unload different storage engines based on their needs, using commands like SHOW ENGINES. This offers flexibility in optimizing database performance.

```text
mysql> show engines;
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
| Engine             | Support | Comment                                                        | Transactions | XA   | Savepoints |
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
| ARCHIVE            | YES     | Archive storage engine                                         | NO           | NO   | NO         |
| BLACKHOLE          | YES     | /dev/null storage engine (anything you write to it disappears) | NO           | NO   | NO         |
| MRG_MYISAM         | YES     | Collection of identical MyISAM tables                          | NO           | NO   | NO         |
| FEDERATED          | NO      | Federated MySQL storage engine                                 | NULL         | NULL | NULL       |
| MyISAM             | YES     | MyISAM storage engine                                          | NO           | NO   | NO         |
| PERFORMANCE_SCHEMA | YES     | Performance Schema                                             | NO           | NO   | NO         |
| InnoDB             | DEFAULT | Supports transactions, row-level locking, and foreign keys     | YES          | YES  | YES        |
| MEMORY             | YES     | Hash based, stored in memory, useful for temporary tables      | NO           | NO   | NO         |
| CSV                | YES     | CSV storage engine                                             | NO           | NO   | NO         |
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
9 rows in set (0.00 sec)
```

#### 2.2.Overview of [`InnoDB`](https://dev.mysql.com/doc/refman/8.0/en/innodb-storage-engine.html)

- **InnoDB is the default and widely used**: It became the default storage engine in MySQL 5.5 and later, known for its reliability and performance.

- **ACID compliance ensures data integrity**: InnoDB supports [`ACID-compliant`](https://dev.mysql.com/doc/refman/8.0/en/mysql-acid.html) properties, providing features like commits, rollback, and crash recovery to protect user data.

- **Performance and scalability features**: InnoDB uses row-level locking and clustered indexes for improved concurrency and reduced I/O, making it suitable for handling large datasets.

#### 2.3.Overview of [`MyISAM`](https://dev.mysql.com/doc/refman/8.0/en/myisam-storage-engine.html)

- **MyISAM prioritizes speed and compression**: This engine is optimized for read operations and offers efficient compression, making it suitable for applications with minimal write operations.

- **Lacks full ACID compliance**: MyISAM doesn't fully support [`ACID-compliant`](https://dev.mysql.com/doc/refman/8.0/en/mysql-acid.html) properties, which can impact data integrity in situations with concurrent transactions.

- **Suitable for specific use cases**: MyISAM is a good choice for read-heavy applications, data warehousing, and situations where full transaction support isn't critical. Its full-text indexing is valuable for complex search operations on text data.

#### 2.4.Overview of [`MEMORY`](https://dev.mysql.com/doc/refman/8.0/en/memory-storage-engine.html)

- **RAM-based for speed**: The Memory engine stores data in RAM, providing extremely fast access with no disk I/O. This makes it ideal for temporary data and lookup tables where speed is critical.

- **Volatile storage**: Data stored in Memory tables is lost when the MySQL server restarts. This engine is not suitable for persistent data storage.

- **Limitations and use cases**: Memory tables have limited storage capacity, don't support [`BLOB/TEXT`](https://dev.mysql.com/doc/refman/8.0/en/blob.html) data types, and use table-level locking. They are best suited for caching, lookup tables, and temporary data processing.

#### 2.5.Overview of [`ARCHIVE`](https://dev.mysql.com/doc/refman/8.0/en/archive-storage-engine.html)

- **Optimized for historical data**: The Archive engine is designed for storing large volumes of historical data efficiently, often used for logging and archiving purposes.

- **High-speed insertion and compression**: It excels at inserting data quickly and compresses data effectively to minimize storage space.

- **Limited functionality**: The Archive engine supports only INSERT, REPLACE, and SELECT operations. It doesn't allow for DELETE or UPDATE operations, and it doesn't support indexes. This makes it unsuitable for transactional workloads or frequent data updates.

#### 2.6.Overview of [`BLACKHOLE`](https://dev.mysql.com/doc/refman/8.0/en/blackhole-storage-engine.html)

- **Data sink for testing and replication**: The BLACKHOLE engine acts like a "black hole" for data, accepting it but not storing it. This can be useful for testing query performance without actual storage or for specific replication setups.

- **Filtering in replication**: In a master-slave replication setup, a server using the BLACKHOLE engine can act as an intermediary. It receives data from the master, applies replication filters (like `replicate-do-*` and `replicate-ignore-*` rules), and passes the filtered data to the slave.

- **Performance testing and diagnostics**: By comparing performance with and without the BLACKHOLE engine, you can isolate the overhead of binary logging and identify performance bottlenecks unrelated to storage.

#### 2.7.Overview of [`CSV`](https://dev.mysql.com/doc/refman/8.0/en/csv-storage-engine.html)

- **CSV file-based storage**: The CSV engine stores data in plain text files with comma-separated values, making it easy to exchange data with other applications that support CSV.

- **Limited functionality**: This engine doesn't support indexing or partitioning, which can limit performance for large datasets or complex queries. It also requires all columns to have the `NOT NULL` attribute.

- **Use cases for data exchange**: The CSV engine is primarily used for importing and exporting data between MySQL and other applications or for situations where data needs to be easily readable in a plain text format.

#### 2.8.Overview of [`MERGE (MSG_MYISAM)`](https://dev.mysql.com/doc/refman/8.0/en/merge-storage-engine.html)

- **Virtual merging of MyISAM tables**: The Merge engine (also known as MRG_MyISAM) allows you to treat multiple MyISAM tables as a single unit, providing a unified view of their data.

- **Benefits for data warehousing**: This engine is often used in data warehousing environments where large volumes of data need to be managed across multiple tables. It can help overcome storage limitations of individual MyISAM tables.

- **Limitations and constraints**: Merge tables don't support partitioning, and all underlying MyISAM tables must have identical column structures. They are also subject to the limitations of the MyISAM engine itself, such as limited transaction support.

#### 2.9.Overview of [`FEDERATED`](https://dev.mysql.com/doc/refman/8.0/en/federated-storage-engine.html)

- **Access remote databases**: The Federated engine allows you to access tables on remote MySQL servers, making it seem like the data is local. This can be useful for distributed database scenarios.

- **Limited practicality and potential issues**: While it offers flexibility, the Federated engine has historically been a source of problems and performance limitations. It was intended to compete with features in enterprise databases like SQL Server and Oracle, but it fell short.

- **Disabled by default**: Due to its limitations and potential issues, the Federated engine is disabled by default in MySQL. Enabling it requires starting the server with specific options.

#### 2.10.Overview of [`PERFORMANCE_SCHEMA`](https://dev.mysql.com/doc/refman/8.0/en/performance-schema.html)

- **Built-in performance monitoring**: PERFORMANCE_SCHEMA acts like an internal monitoring system, collecting data about various events and operations within the MySQL server (e.g., thread activity, mutex waits, query execution).

- **Detailed insights with low overhead**: It provides granular performance metrics with minimal impact on the server's performance, allowing you to analyze resource usage, identify bottlenecks, and optimize queries.

- **Accessible through SQL queries**: Performance data is stored in tables within the `performance_schema` database, and you can access this data using standard SQL queries to retrieve and analyze the information.

#### 2.11.Overview of [`NDB Cluster`](https://dev.mysql.com/doc/refman/8.0/en/mysql-cluster-overview.html)

- **NDB Cluster for high availability and in-memory performance**: This engine provides high availability and data persistence with its in-memory storage approach. It's suitable for applications that require constant uptime and fast data access.

- **Specialized use cases for different engines**: The text highlights how different storage engines are better suited for specific needs (e.g., InnoDB for transactional data, MyISAM for read-heavy operations, Memory for temporary data).

- **Choosing the right engine is crucial**: Understanding the strengths and limitations of each storage engine helps in selecting the most appropriate one for your application's requirements, whether it's high availability, transaction support, or read performance.

## III.[Improved features in MySQL 8](https://dev.mysql.com/doc/refman/8.0/en/mysql-nutshell.html)

- **MySQL 8 is a major release**: It includes significant updates and addresses previous issues, marking a substantial advancement from version 5.7.

- **Versions 6 and 7 weren't forgotten**: Version 6.0 was part of a transition to a new release cycle, and 7.0 was designated for the clustering version of MySQL.

- **New features enhance functionality**: MySQL 8 introduces a range of new features (as shown in the diagram), including improvements to indexing, character sets, [GIS support](https://dev.mysql.com/doc/refman/8.0/en/spatial-types.html), and more. These enhancements offer compelling reasons to upgrade.

![Improved features in MySQL 8](<./Improved features in MySQL 8.png>)

### 1.[Transactional data dictionary](https://dev.mysql.com/doc/refman/8.0/en/data-dictionary-transactional-storage.html)

- **Centralized and transactional**: The data dictionary, which stores metadata about the database (tables, columns, etc.), is now stored in transactional tables within the database itself. This eliminates the need for separate metadata files like `.frm` files.

- **Improved performance and reliability**: This change brings performance benefits by allowing data dictionary information to be cached in memory. It also improves reliability and crash recovery by making data dictionary operations transactional.

- **Simplified management**: Centralizing metadata in a transactional data dictionary makes it easier to manage, add new features, and maintain the database overall.

### 2.[Roles](https://dev.mysql.com/doc/refman/8.0/en/roles.html)

- **Roles streamline privilege management**: MySQL 8 introduces roles, which are essentially collections of privileges. This allows you to group related permissions and assign them to multiple users easily.

- **Simplified updates and maintenance**: Instead of granting or revoking individual privileges for each user, you can now manage privileges at the role level. Any changes to a role automatically apply to all users assigned to that role.

- **Increased efficiency and flexibility**: Roles make it much easier to handle scenarios with many users, especially when those users share common permissions. This saves time and reduces the risk of errors compared to managing privileges individually.

### 3.[InnoDB auto increment](https://dev.mysql.com/doc/refman/8.0/en/innodb-auto-increment-handling.html)

- **Persistent auto-increment counter**: In MySQL 8, the auto-increment counter is now persisted in the redo log and system table, ensuring that the counter value survives server restarts and crashes. This improves reliability and prevents data loss.

- **Prevents duplicate entry errors**: The persistent counter helps avoid situations where auto-increment values could be duplicated after updates or server restarts, ensuring data integrity.

- **Faster recovery**: By storing the auto-increment counter in the data dictionary table, InnoDB can quickly initialize the counter on server restart without needing to scan the table for the maximum value, leading to faster recovery times.

### 4.[Invisible indexes](https://dev.mysql.com/doc/refman/8.0/en/invisible-indexes.html)

- **Test performance without dropping indexes**: Invisible indexes allow you to "hide" an index from the query optimizer, effectively simulating its removal without actually deleting it. This is great for testing performance impacts.

- **Avoid costly rebuilds**: Instead of dropping and recreating indexes (which can be expensive on large tables), you can make them invisible to see how queries perform. If the index is needed, simply make it visible again.

- **Easy to manage**: You can easily toggle the visibility of an index using the `INVISIBLE` and `VISIBLE` keywords in an `ALTER TABLE` statement. This provides flexibility in managing and testing index usage.

### 5.[Improving descending indexes](https://dev.mysql.com/doc/refman/8.0/en/descending-indexes.html)

- **Optimized descending indexes**: In MySQL 8, descending indexes are now scanned in forward order, unlike in previous versions where they were scanned in reverse. This optimization significantly improves performance for queries using descending indexes.

- **Improved efficiency for multiple column indexes**: This change also benefits multiple column indexes where some columns have ascending order and others have descending order. The optimizer can now choose the most efficient scan direction for each column, leading to better overall performance.

- **Enhanced query performance**: By optimizing descending index scans, MySQL 8 can execute queries involving those indexes more efficiently, resulting in faster data retrieval and improved application performance.

### 6.[The `SET PERSIST` variant](https://dev.mysql.com/doc/refman/8.0/en/persisted-system-variables.html)

- **Persistent server variables**: MySQL 8 introduces the `SET PERSIST` command, which allows you to set server variables and have those settings persist across server restarts. This eliminates the need to reconfigure variables every time the server starts.

- **Simplified configuration**: Previously, you had to use `SET GLOBAL` to change server variables, but these changes were lost after a restart. `SET PERSIST` offers a more convenient way to make lasting configuration changes.

- **Example**: Instead of `SET GLOBAL max_connections = 1000`, you can now use `SET PERSIST max_connections = 1000` to make the `max_connections` setting permanent. This simplifies server administration and ensures consistent configuration.

### 7.[Expanded GIS support](https://dev.mysql.com/doc/refman/8.0/en/spatial-analysis-functions.html)

- **Support for geographic coordinate systems**: MySQL 8 now supports SRS, allowing you to work with geographic data that's accurately referenced to locations on Earth. This wasn't possible in previous versions, which only supported a simple 2D plane.

- **Enhanced spatial analysis**: SRS enables more accurate and meaningful spatial analysis by considering the Earth's shape and different coordinate systems. This is crucial for applications involving maps, location-based services, and geographic data processing.

- **Metadata storage in data dictionary**: Information about spatial reference systems is stored in the data dictionary, making it easy to manage and access. This improves the organization and consistency of spatial data within the database.

### 8.[Extended bit-wise operations](https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html)

- **Support for binary data types**: MySQL 8 extends bit-wise operations to work with binary data types like `BINARY`, `VARBINARY`, and `BLOB`. This was previously limited to `BIGINT` (64-bit integer) in MySQL 5.7.

- **Handles data larger than 64 bits**: This enhancement allows you to perform bit-wise operations on data exceeding 64 bits in size, eliminating the need for potentially inaccurate type casting that was necessary in older versions.

- **More efficient and accurate**: By directly supporting binary data types, MySQL 8 makes bit-wise operations more efficient and accurate for a wider range of use cases involving binary data manipulation.

### 9.[InnoDB Memcached](https://dev.mysql.com/doc/refman/8.0/en/innodb-memcached.html)

- **Multiple get operations**: The plugin now supports fetching multiple key-value pairs in a single memcached query. This reduces communication overhead and improves read performance by minimizing the number of round trips to the server.

- **Range queries**: InnoDB Memcached now supports range queries, allowing you to efficiently retrieve values within a specified range of keys. This simplifies data retrieval for certain access patterns.

- **Enhanced caching capabilities**: These enhancements make InnoDB Memcached a more versatile and efficient caching solution, particularly for applications that require retrieval of multiple keys or range-based data access.

### 10.[NOWAIT and SKIP LOCKED](https://dev.mysql.com/doc/refman/8.0/en/innodb-locking-reads.html)

- **Avoid waiting for locks**: When a transaction needs to access a row that's locked by another transaction, `NOWAIT` and `SKIP LOCKED` provide ways to avoid waiting.

  - `NOWAIT` immediately returns an error if the row is locked.

  - `SKIP LOCKED` skips over locked rows and continues processing the rest of the query.

- **Improved concurrency and responsiveness**: These options can improve concurrency by preventing transactions from being blocked by long-held locks. They also make applications more responsive by avoiding unnecessary delays.

- **Use cases**: `NOWAIT` is useful when you need immediate access to data and can handle potential lock conflicts. `SKIP LOCKED` is suitable for scenarios where you can process some data even if some rows are locked, such as in queue processing or batch jobs.

### 11.[JSON](https://dev.mysql.com/doc/refman/8.0/en/json.html)

- **More functions for JSON data**: MySQL 8 adds several new functions to work with JSON data, including aggregation functions like `JSON_OBJECTAGG()` and `JSON_ARRAYAGG()`. These functions make it easier to generate and manipulate JSON documents within MySQL.

- **Server-side JSON manipulation**: With these new functions, you can perform more complex JSON operations directly within the database server, reducing the need to process JSON data in your application code.

- **Improved efficiency and flexibility**: The enhanced JSON support in MySQL 8 provides greater flexibility and efficiency when working with JSON documents, making it a more powerful tool for modern applications that often utilize JSON for data exchange.

### 12.[Cloud](https://dev.mysql.com/doc/refman/8.0/en/innodb-dedicated-server.html)

- **Automatic configuration for virtual servers**: The `innodb_dedicated_server` option allows MySQL 8 to automatically detect and utilize the resources available in a virtual server environment. This simplifies configuration and optimizes performance without manual tuning.

- **Reduced need for shell access**: With the combination of `innodb_dedicated_server` and `SET PERSIST`, you can configure many MySQL settings without needing direct shell access to the server. This enhances security by minimizing the need for potentially risky access privileges.

- **Cloud-ready database**: These features demonstrate how MySQL 8 is adapting to the increasing use of cloud and virtualization technologies. They make it easier to deploy and manage MySQL instances in cloud environments, improving efficiency and security.

### 13.[Resource management](https://dev.mysql.com/doc/refman/8.0/en/resource-groups.html)

- **Fine-grained control over resource allocation**: MySQL 8 introduces resource groups, allowing you to allocate resources (currently CPU time) to different groups of threads. This provides more control over how server resources are used by different workloads.

- **Improved performance and efficiency**: By assigning threads to specific resource groups, you can prioritize critical tasks and ensure that they have the necessary resources to perform optimally. This can lead to better overall database performance and resource utilization.

- **Enhanced workload management**: This feature enables more sophisticated workload management within MySQL itself. You can fine-tune resource allocation based on the needs of different applications or tasks, optimizing the server for various usage patterns.

## IV. Benefits of using MySQL 8

- **Comprehensive feature set**: MySQL provides a wide range of features that make it a robust and versatile database solution. This includes features for data security, scalability, performance optimization, and more.

- **Proven reliability and performance**: MySQL has a long history of use in demanding production environments. It's known for its stability, speed, and ability to handle large datasets and high query volumes.

- **Open-source with strong community support**: MySQL's open-source nature makes it cost-effective and accessible. It also benefits from a large and active community that provides support, resources, and contributions to its ongoing development.

### 1.[Security](https://dev.mysql.com/doc/refman/8.0/en/security.html)

- **Robust security measures**: MySQL offers a comprehensive security framework, including access control management, encryption for user passwords, and secure authentication mechanisms. These features help protect sensitive information from unauthorized access.

- **Access control and roles**: MySQL allows granular control over user access and privileges. You can grant and revoke specific permissions to individual users or use roles to manage permissions for groups of users efficiently.

- **Data encryption**: User passwords are stored using strong encryption algorithms, adding a layer of protection against password theft and unauthorized access. MySQL also supports encrypted connections to further secure data in transit.

### 2.Scalability

- **Horizontal and vertical scalability**: MySQL supports both horizontal scaling (distributing data and queries across multiple servers) and vertical scaling (adding more resources to a single server). This provides flexibility in how you scale your database to meet growing needs.

- **Handles increasing data volumes and user load**: MySQL's scalability features allow it to handle increasing amounts of data and user traffic without significant performance degradation. This is crucial for applications that experience rapid growth or unpredictable spikes in usage.

- **Adapts to changing needs**: Whether you need to accommodate more data, handle more concurrent users, or improve query performance, MySQL's scalability options provide a way to adapt your database infrastructure to meet those demands.

### 3.An open source relational database management system

- **Flexibility and Customization**: MySQL's open-source license allows you to freely access and modify the source code. This enables customization, debugging, and optimization to suit your specific needs.

- **Community-driven development**: The open-source model fosters a large and active community of developers who contribute to MySQL's improvement, provide support, and share knowledge.

- **Cost-effective solution**: MySQL is free to use, distribute, and modify, making it a cost-effective choice for businesses and developers compared to proprietary database systems. However, distributing modified versions may require licensing, depending on the extent of the changes.

### 4.High performance

- **Optimized for speed**: MySQL is designed with performance in mind, incorporating features like caching, indexing, and query optimization to ensure fast data retrieval and efficient transaction processing.

- **Scalability for demanding workloads**: MySQL's scalability features, including replication and clustering, allow it to handle demanding workloads and high concurrency without sacrificing performance.

- **Continuous improvements**: MySQL 8 introduces further performance enhancements, such as optimized indexing in the performance schema, to further speed up data retrieval and overall database operations.

### 5.High availability

- **Minimized downtime**: MySQL's clustering and replication capabilities provide high availability by allowing the system to quickly recover from failures and maintain continuous operation.

- **Automatic failover**: If one server in a cluster fails, MySQL can automatically redirect user requests to another functioning server, minimizing disruption to applications and users.

- **Increased reliability**: These high availability features make MySQL a reliable choice for applications where downtime is unacceptable, ensuring business continuity and preventing revenue loss.

### 6.Cross-platform capabilities

- **Wide range of supported platforms**: MySQL runs on many operating systems, including Windows, Linux, Solaris, and more. This flexibility allows you to use MySQL in diverse environments and integrate it with existing infrastructure.

- **Extensive API support**: MySQL provides APIs for a variety of programming languages like PHP, C++, Java, Python, and Perl. This makes it easy to develop applications that interact with MySQL databases using your preferred language.

- **Popular choice for web applications**: MySQL is a core component of the widely used LAMP stack (Linux, Apache, MySQL, PHP), which powers many web applications worldwide. This demonstrates its popularity and suitability for web development.

## V.Limitations of MySQL 8

### 1.Number of tables or databases

- **No inherent limit on tables/databases**: MySQL 8 doesn't have a fixed limit on the number of databases or tables you can create. You can theoretically have a very large number.

- **Operating system limits may apply**: The practical limit is often determined by the operating system's file handling capabilities and available resources.

- **InnoDB's capacity**: The InnoDB storage engine, commonly used in MySQL, can handle up to 4 billion tables, which is a massive number for most use cases.

### 2.Table size

You may hit maximum table size limit, which is not restricted from MySQL 8; however, it
may be because of operating system filesystem limits.

### 3.Joins

In a single join, one can use 61 tables, which can be referred. It is also applicable to the
tables that are referenced in view definition. Joins that are part of subqueries and views are
also considered to be part of the limitation.

### 4.Table column count

The table column for each table in MySQL 8 has a limit of 4096 columns. It might vary
based on a few other factors for columns count limit, as stated in the following section.

### 5.Row size

MySQL tables have a limit of 65,535 bytes for a row, although storage engines such as InnoDB are capable of supporting larger chunks.

### 6.`InnoDB` storage engine

Limitations on `InnoDB` storage engine are what we will talk about a bit more specifically as `InnoDB` now with MySQL 8 will play a prominent role

### 7.Limitations of `InnoDB` storage engine

We will have a quick glance at a few of the limitations of `InnoDB` storage engine:

- The number of indexes supported can be maximum 64 for a table

- For tables that use compressed or dynamic row format; 3072 is the index key prefix length limit

- For tables that use compact or redundant row format; 767 is the index key prefix length limit

- Total columns in a table, which includes virtual generated columns, are limited to a maximum of 1,017

- 16 columns is the maximum permitted for multi-column indexes

- The combined `InnoDB` log file size cannot exceed 512 GB

- Maximum table size supported by `InnoDB` is 256 TB

- AdminAPI is not supported while using unix socket connections

- Multi-byte characters might give you unreliable aligned columns while formatting of results in `InnoDB` clusters

### 8.Restrictions

We will now have a quick glance at a few of the restrictions of the `InnoDB` storage engine:

- **Delete from tablename**: It doesn't actually delete the complete table, instead it deletes each row of the table one after another.

- **Show table status**: It wouldn't provide you accurate data all the time; it provides estimates.

- When counting rows, the number of rows provided by `count(*)` is not accurate because of concurrency; it would count only those counts visible to transactions currently available.

- If there is multiple `analyze table` queries executed, later one will be blocked until the first one gets completed.

- `InnoDB` keeps an exclusive lock on the index at the end associated with the `auto_increment` column.

- In a case the `auto_increment` integer runs out of the value; the following insert operations would show us duplicate-key errors.

- Foreign keys that are cascaded cannot activate triggers.

- There are a few column names reserved by MySQL that `InnoDB` uses for internal purposes. The following are a few such column names:

  - `DB_ROW_ID`
  - `DB_TRX_ID`
  - `DB_ROLL_PTR`
  - `DB_MIX_ID`

  We might come across output shown in the following example in case of such
  reserved column names used:

  ```mysql-shell
  mysql> CREATE TABLE chintan (c1 INT, db_row_id INT) ENGINE=INNODB;
  ERROR 1166 (42000): Incorrect column name 'db_row_id'
  ```

- `InnoDB` locks are released immediately after the transaction is aborted or committed, which is held by a transaction.

- The addition of table locks are not supported, as locks are implicit to `commit` and `unlock tables`

### 9.Limitations of data dictionary

- Individual `MyISAM` tables for backup and restore are not supported by merely copying the files.

- Manually created directories for databases are not supported by MySQL 8. For instance, using `mkdir` would have no impact on MySQL server data dictionary.

- `DDL` operations would take more time than expected because such operations are written to storage, undo logs and redo instead of `.frm` files as what we would have seen in prior versions of MySQL.

### 10.Limitations of group replication in MySQL8

- **Large transactions**: Transactions that result to GTID contents cannot be replicated between the rest of the members of the group if they're too large. It is suggested to use smaller chunks of data that cannot be replicated in around five seconds to group members to avoid failures.

- **Cluster from a group**: If you try to create clusters from an existing group replication setup it will result in an error as the instance would already be part of a replication group. This is noticed currently only in MySQL's wizard mode only; an alternative solution for the issue is to disable wizard mode.

- **Serializable isolation level**: Serializable isolation level is not supported when multi-primary groups are used, which is the default configuration.

- **DDL and DML operations**: If there is concurrent DDL and DML operations executed against the same data object but on different servers is not supported when multi-primary group mode is used.

- **Replication checksum**: Currently MySQL design limitations create restrictions of having replication event checksums

### 11.Limitations of partitioning

We will be discussing limitations of partitioning in this section.

### 12.Constructs prohibition

The following are the constructs that are not allowed in expressions of partitions:

- Declared variables
- User variables
- Stored procedures
- Stored functions
- UDFs
- Plugins

### 13.Operators

There are a few operators that are not permitted in partition expressions such as `<<`, `>>`, `|`, `&`, `~` and `^`. Results for arithmetic operators such as `+`, `-` and `*`must have an integer value or `NULL`.

### 14.Limitations of partitioning on tables

- The maximum number of partitions supported by MySQL 8 for a table is 8192. This limit also considers sub-partitions.

- Fulltext index and search is not supported on partitioned tables.

- Tables that are temporary cannot be partitioned.

- Log tables can't be partitioned.

- Foreign keys are not supported on partitioned `InnoDB` storage engine.

- The data type of partition keys should be an integer column or can be an expression to an integer. Expression or column values may be `NULL`; however, expressions that include `ENUM` are not supported.

- Upgrading partitioned tables that have been partitioned by `KEY` would have to be reloaded, which stands true other than the `InnoDB`storage engine.

## VI.Use cases of MySQL

- **Data-driven insights**: MySQL empowers businesses to extract valuable insights from their data, regardless of the data's origin or complexity. This allows organizations to make informed decisions, improve operations, and gain a competitive edge.

- **Versatility for diverse applications**: MySQL's adaptability makes it suitable for a wide range of applications, from small-scale websites to large enterprise systems. It can handle diverse data types and support various use cases, making it a valuable tool for many organizations.

- **Focus on actionable information**: MySQL's features and capabilities are geared towards enabling businesses to not just store data, but to analyze it, understand it, and use it to drive meaningful actions and achieve their goals.

![Improved features in MySQL 8](<./Use cases of MySQL.png>)

### 1.Social media

- **MySQL at scale**: Facebook's use of MySQL demonstrates its ability to handle massive datasets and high traffic loads, even for complex applications with diverse data needs.

- **Customization and optimization**: Facebook's development of RocksDB on top of InnoDB showcases the flexibility of MySQL's architecture and the potential for customization to meet specific performance and storage requirements.

- **Continued relevance**: While Facebook has implemented custom solutions to address its unique needs, MySQL remains a crucial component of their infrastructure and a widely used database system for various other applications.

### 2.Government

- **Cost-effective solution for governments**: MySQL's open-source nature makes it a cost-effective choice for government agencies, allowing them to maximize their IT budgets and invest in other critical areas.

- **Proven reliability for critical systems**: The US Navy's use of MySQL for flight planning demonstrates its ability to handle mission-critical applications that require 24/7 availability and data integrity.

- **Wide adoption in the public sector**: MySQL's presence in various government implementations worldwide showcases its versatility and suitability for diverse public sector needs, from managing citizen data to supporting critical infrastructure.

### 3.Media and entertainment

- **Handling massive scale**: YouTube's reliance on MySQL shows its ability to manage the storage and retrieval of massive amounts of video data and user interactions, serving millions of users concurrently.

- **Optimization with Vitess**: YouTube's development of Vitess, a proxy layer for MySQL, illustrates how the database can be optimized for specific needs. Vitess helps distribute load, improve query routing, and enhance scalability.

- **Replication and caching**: YouTube leverages MySQL's replication features to ensure high availability and data redundancy. Caching is also crucial for optimizing performance and reducing database load, especially for frequently accessed data.

### 4.Fraud detection

- **Real-time analysis for proactive prevention**: MySQL's ability to analyze transactions and identify suspicious patterns in real-time allows businesses to detect and prevent fraud before significant losses occur. This proactive approach is critical for minimizing financial damage and maintaining customer trust.

- **Scalability and performance for demanding needs**: As demonstrated by PayPal's use case, MySQL can handle the demands of high-volume transaction processing and fraud detection systems, providing the necessary scalability and performance to analyze massive datasets and protect millions of users.

- **Adaptable for various fraud detection techniques**: MySQL's versatility makes it suitable for implementing various fraud detection techniques, including rule-based systems, anomaly detection algorithms, and machine learning models. This allows businesses to tailor their fraud prevention strategies to their specific needs and risks.

### 5.Business mapping

- **Mission-critical reliability**: Netflix's use of MySQL for its billing system highlights its reliability and ability to handle sensitive financial data with high accuracy and availability.

- **Scalability for massive datasets**: MySQL's ability to manage billions of rows of data, accumulated over two decades, demonstrates its scalability and suitability for long-term data storage and processing.

- **Successful migration and compliance**: Netflix's successful migration from Oracle to MySQL with minimal downtime shows that MySQL can be a viable alternative for large-scale systems, even with strict compliance requirements.

### 6.E-commerce

- **Supporting diverse industries**: MySQL's versatility and scalability make it a valuable tool across a wide range of industries, from technology and finance to healthcare and government.

- **Driving innovation**: MySQL plays a crucial role in supporting innovative applications and services, such as Uber's transportation platform, that are changing the way we live and interact with the world.

- **Hidden influence**: Even though we might not always be aware of it, MySQL is often the underlying engine powering many of the applications and services we use daily, making it an integral part of our modern digital landscape.
