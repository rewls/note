# Oracle Database Free Release 23ai (23.4.0.0) Container Image Documentation

- Oracle Database 23ai Free is the developer edition of the industry-leading relational database server.

- The Oracle Database Free server Container image contains Oracle Database Free Release 23ai (23.4.0.0) running on Oracle Linux 8.

- This image contains a default database in a multitenant configuration with one pluggable database.

## Using This Image

### Starting an Oracle Database Server Instance

- The Oracle Database 23ai Free server Container image contains a pre-built database, so the startup time is very fast.

- To start an Oracle Database server instance, run the following command where, `<oracle-db>` is the name of the container:

```shell
$ docker run -d --name <oracle-db> container-registry.oracle.com/database/free:latest
```

- When the container is started, a random password is used for the `SYS`, `SYSTEM` and `PDBADMIN` users.

- This is termed as the default password.

### Note

- To change the default password, see: [Changing the Default Password for SYS User](#changing-the-default-password-for-sys-user)

- To learn about advanced use cases, see: [Custom Configurations](#custom-configuration)

- The Oracle Database server is ready to use when the `STATUS` field shows `(healthy)` in the `docker ps` output.

## Custom Configurations

- To facilitate custom configurations, the Oracle Database server container provides configuration parameters that you can use when starting the container.

- For example, this is the detailed `docker run` command supporting all custom configurations:

```
podman run --name <container name> \
-P | -p <host port>:1521 \
-e ORACLE_PWD=<your database passwords> \
-e ORACLE_CHARACTERSET=<your character set> \
-e ENABLE_ARCHIVELOG=true \
-e ENABLE_FORCE_LOGGING=true \
-v [<host mount point>:]/opt/oracle/oradata \
container-registry.oracle.com/database/free:latest

Parameters:
   --name:        The name of the container (default: auto generated)
   -P | -p:       The port mapping of the host port to the container port.
                  Only one port is exposed: 1521 (Oracle Listener)
   -e ORACLE_PWD: The Oracle Database SYS, SYSTEM and PDB_ADMIN password (default: auto generated)
   -e ORACLE_CHARACTERSET:
                  The character set to use when creating the database (default: AL32UTF8)
   -e ENABLE_ARCHIVELOG:
                  To enable archive log mode when creating the database (default: false)
   -e ENABLE_FORCE_LOGGING:
                  To enable force logging mode when creating the database (default: false)
   -v /opt/oracle/oradata
                  The data volume to use for the database.
                  Has to be writable by the Unix "oracle" (uid: 54321) user inside the container.
                  If omitted the database will not be persisted over container recreation.
   -v /opt/oracle/scripts/startup
                  Optional: A volume with custom scripts to be run after database startup.
                  For further details see the "Running scripts after setup and on startup" section below.
   -v /opt/oracle/scripts/setup
                  Optional: A volume with custom scripts to be run after database setup.
                  For further details see the "Running scripts after setup and on startup" section below.
```

## Changing the Default Password for SYS User

- To change the password for these accounts, use the `docker exec` command, to run the `setPassword.sh` script that is found in the container.

```shell
$ docker exec <oracle-db> ./setPassword.sh <your-password>
```

## Database Alert Logs

- You can access the database alert log by using the following command, where `<oracle-db>` is the name of the container:

```shell
$ podman logs <oracle-db>
```

## Connecting from Within the Container

- You can connect to the Oracle Database server by running a SQL*Plus command from within the container using one of the following commands:

```shell
$ podman exec -it <oracle-db> sqlplus sys/<your_password>@FREE as sysdba
$ podman exec -it <oracle-db> sqlplus system/<your_password>@FREE
$ podman exec -it <oracle-db> sqlplus pdbadmin/<your_password>@FREEPDB1
```

## Connecting from Outside the Container

- By default, Oracle Database exposes port 1521 for Oracle client connections, using Oracle's SQL*Net protocol.

- SQL*Plus or any Oracle Java Database Connectivity (JDBC) client can be used to connect to the database server from outside of the container.

- To connect from outside of the container, start the container with the -P option, as described in the detailed Podman run command in the [Custom Configurations](custom-configurations) section.

- Discover the mapped port by running the following command:

```shell
$ docker port <oracle-db>
```

- To connect from outside of the container using SQL*Plus, run the following commands:

```shell
# To connect to the database at the CDB$ROOT level as sysdba:
$ sqlplus sys/<your password>@//localhost:<port mapped to 1521>/FREE as sysdba
# To connect as non sysdba at the CDB$ROOT level:
$ sqlplus system/<your password>@//localhost:<port mapped to 1521>/FREE
# To connect to the default Pluggable Database (PDB) within the FREE Database:
$ sqlplus pdbadmin/<your password>@//localhost:<port mapped to 1521>/FREEPDB1
```
