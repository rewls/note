# 2 Sample Databases for SQLite

> https://database.guide/2-sample-databases-sqlite/

## 1. The Chinook Database

- The Chinook database was created as an alternative to the Northwind database.

- It represents a digital media store, including tables for artists, albums, media tracks, invoices and customers.

- The Chinook database is available on GitHub.

- It's available for various DBMSs including MySQL, SQL Server, SQL Server Compact, PostgreSQL, Oracle, DB2, and of course, SQLite.

### Install the Chinook Database

- You can install the Chinook database in SQLite by running the SQL script available on GitHub.

- It's quite a large script, so you might find it easier to run it from a file.

- First, save the Chinook_Sqlite.sql script to a directory on your computer.

    - https://raw.githubusercontent.com/lerocha/chinook-database/master/ChinookDatabase/DataSources/Chinook_Sqlite.sql

- You can create a database called Chinook by connecting to SQLite with the following command:

    ```shell
    $ sqlite3 Chinook.db
    ```

- To run the script from the file, use the following command:

```shell
.read Chinook_Sqlite.sql
```

- You can verify that it created the database by selecting some data from a table:

    ```sql
    select * from Artist limit 10;
    ```
