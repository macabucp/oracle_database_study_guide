# Creating and Operating Oracle Database 12c

## Oracle Database 12c: OCA Exam Objectives Covered in This Chapter

### Oracle Software Installation Basics
- **Plan for an Oracle Database software installation.**

### Installing Oracle Database Software
- **Install the Oracle Database software.**

### Creating an Oracle Database Using DBCA
- **Create a database using the Database Configuration Assistant (DBCA).**
- **Generate database creation scripts using DBCA.**
- **Manage database design templates using DBCA.**
- **Configure database options using DBCA.**

### Oracle Database Instance
- **Understand initialization parameter files.**
- **Start up and shut down an Oracle database instance.**
- **View the alert log and access dynamic performance views.**

## Chapter Overview

As a DBA, you are responsible for creating and managing Oracle databases and services within your organization. Oracle provides a comprehensive set of tools to help DBAs perform these tasks effectively. Understanding these tools and their proper usage is crucial for database administration.

Oracle utilizes Java-based tools to manage Oracle Database 12c, ensuring a consistent user experience across different platforms. In this chapter, you'll learn to use the Oracle Database Configuration Assistant (DBCA) to create and delete Oracle databases, manage database design templates, and modify database options.

### Key Topics Covered:

1. **Using Oracle Database Configuration Assistant (DBCA):**
   - DBCA is used for creating and deleting Oracle databases.
   - It can also generate scripts for database creation, manage database design templates, and configure database options.

2. **Database Operations:**
   - After creating a database with DBCA, you will learn to shut down and restart the database for configuration changes, applying patches, and server maintenance.
   - Various database startup and shutdown options will be explained, along with the appropriate circumstances for their use.

3. **Oracle Data Dictionary:**
   - Understanding the creation and location of the Oracle data dictionary.
   - How to use and manage the data dictionary effectively.

4. **Initialization Parameter Files:**
   - Discussion on managing and understanding initialization parameter files.
   - How to use these files to view and manage the database alert log and access dynamic performance views.

This chapter equips you with the essential knowledge and tools to effectively manage Oracle Database 12c, ensuring that you can perform installations, configurations, and ongoing database management with confidence.

# Oracle Database 12c Software Installation

## Oracle Universal Installer (OUI)
- **OUI Overview:** A Java-based graphical tool used to install Oracle software. OUI provides a consistent look and feel across all platforms.
- **Installation Capabilities:** Can install Oracle software and optionally create an Oracle database during the installation process.

## Planning the Oracle Database 12c Software Install
- **Download Sources:** 
  - Oracle database software is available for download from Oracle's Software Delivery Cloud and patches from My Oracle Support (MOS).
  - Supported platforms include Unix, Linux, and Windows (64-bit edition only).

### Documentation Review
- **Essential Documents to Review:**
  - Installation guide specific to your operating system.
  - General and OS-specific release notes.
  - Quick-start installation guides.

### System Requirements
- **Hardware and Software Specifications:**
  - **Memory:** Minimum 1GB, recommended 2GB+.
  - **Swap Space:** 1.5GB or equal to the amount of RAM.
  - **Temp Space:** 1GB of free space in the `/tmp` directory for Unix systems.
  - **Disk Space:** 6.4GB of free disk space.
  - Unix systems also require kernel parameter adjustments.

### Installation Planning
- **Optimal Flexible Architecture (OFA) Model:** Recommended by Oracle for managing installations, ensuring easier management, upgrades, and backups.
- **Key Planning Considerations:**
  - Determine the operating-system user to own the Oracle software.
  - Decide on disk drive and directory for installation.
  - Plan the directory structure for Oracle software, configuration files, and database.
  - Optimize database file layout for performance and recoverability.

### Creating the Oracle User Account
- **Unix Systems:** Create a Unix user account (commonly named `oracle`, `ora12c`, or `ora121`) and assign to an operating-system group, typically `dba`.
- **Windows Systems:** Use an account with administrative privileges.

### Oracle Inventory
- **Purpose:** Tracks installed Oracle software on the server.
- **Location:**
  - **Unix Systems:** Defined by `/etc/oraInst.loc`.
  - **Windows Systems:** Typically found under `C:\Program Files\Oracle\Inventory`.

### Job Role Separation Using OS Groups
- **OSDBA Group:** Mandatory group for DBA privileges, allowing OS authentication to the database.
- **Other Groups:** Configured for different job roles such as backup, recovery, and encryption key management.

### Naming Volumes and Mount Points
- **Unix Systems:** Use generic names for mount points like `/u01`, `/mnt01`, `/du01`.
- **Windows Systems:** Use standard drive letters (e.g., `C:`, `D:`).

### Creating OFA Directory Paths
- **Environment Variables:**
  - **Unix Systems:** `$ORACLE_BASE`, `$ORACLE_HOME`.
  - **Windows Systems:** `%ORACLE_BASE%`, `%ORACLE_HOME%`.

### Common Non-OFA Environment Variables
- **Examples:** `$ORACLE_SID`, `$TNS_ADMIN`, `$LD_LIBRARY_PATH`, `$PATH`.
- **Usage:** Important for database creation and management.

## Using the Oracle Universal Installer
- **OUI Process:**
  - **Steps:** Unzipping software, performing preinstallation checks, responding to prompts, selecting products, copying files, compiling binaries, and post-installation operations.

### Installation Options
- **Options:**
  - **Create And Configure A Database:** Installs software and creates a new database.
  - **Install Database Software Only:** Installs only the database binaries.
  - **Upgrade An Existing Database:** Installs software and upgrades an existing database.

### Installation Process
- **Preinstallation Checks:** OUI verifies system compatibility and displays the initial installation screen.
- **Installation Choices:** Options include grid installation for RAC, edition selection (Enterprise, Standard, Standard One, Personal), and specifying installation locations.

### Post-Installation Steps
- **Unix Systems:** Execute configuration scripts (`orainstRoot.sh`, `root.sh`) as root to complete the installation.
- **Silent Installation:** Use OUI response files for unattended installations.

## Next Steps
- **Database Creation:** Use the installed Oracle software to create your first database.

# Using DBCA to Create an Oracle 12c Database

The Oracle Database Configuration Assistant (DBCA) is a Java-based tool used to create, manage, and delete Oracle databases. The DBCA offers flexibility and ease of use, allowing DBAs to create databases with a graphical interface or using Oracle-generated XML templates for consistency and repeatability.

## Invoking the Database Configuration Assistant

You can start the DBCA from the command line in Unix (`$ORACLE_HOME/bin/dbca`) or as an application in Windows (`Start ⇒ All Programs ⇒ Oracle Home ⇒ Configuration and Migration Tools ⇒ Database Configuration Assistant`). 

After starting the DBCA, the Operation screen appears (Figure 9.8), offering various options such as creating a database, configuring database options, deleting a database, managing templates, and managing pluggable databases.

### DBCA Database Management Options

| Option                     | Description |
|----------------------------|-------------|
| Create a Database           | Step-by-step creation of a database using templates or custom configurations. |
| Configure Database Options  | Modify server configurations, add database options, or transition from a dedicated to a shared server. |
| Delete a Database           | Remove a database and all associated files. |
| Manage Templates            | Manage database templates for consistent and repeatable database creation. |
| Manage Pluggable Databases   | Manage pluggable databases for multitenant environments. |

### Creating a Database with DBCA

1. **Choose the Creation Mode**:
   - **Create Database With Default Configuration**: A quick setup with minimal inputs.
   - **Advanced Mode**: Offers more customization options for database creation.

2. **Database Templates**:
   - DBCA comes with predefined templates like Data Warehouse and General Purpose or Transaction Processing (Figure 9.10).
   - **Custom Database**: Provides maximum flexibility for customizing tablespaces, components, and configurations.

3. **Database Identification**:
   - **Global Database Name**: A fully qualified name of the database (e.g., `sales.company.com`).
   - **Oracle SID**: The system identification name, typically matching the database name.

4. **Management Options**:
   - Configure Enterprise Manager (EM) for monitoring and managing the database (Figure 9.13).

5. **Database Credentials**:
   - Set passwords for administrative accounts like `SYS` and `SYSTEM` (Figure 9.14).

6. **Network Configuration**:
   - Define or associate the database with a listener for network access (Figure 9.15).

7. **Storage Locations**:
   - Choose between File System and Automatic Storage Management (ASM) for managing disk storage (Figure 9.16).

8. **Recovery and Archiving**:
   - Configure Fast Recovery Area (FRA) and enable archiving options for data protection.

9. **Database Options**:
   - Select additional database components to install, like Oracle JVM, Oracle Text, or Oracle Application Express (Figures 9.17 and 9.18).

10. **Sample Schemas and Custom Scripts**:
    - Optionally include sample schemas like HR, OE, and SH or run custom scripts during database creation (Figure 9.19).

11. **Initialization Parameters**:
    - Configure memory, sizing, character sets, and connection modes (Figures 9.20-9.26).

12. **Creation Options**:
    - Choose to create the database, save the configuration as a template, or generate scripts for manual database creation (Figure 9.28).

### Customizing Storage

The Customize Storage screen (Figure 9.29) allows you to review and modify the locations of data files, control files, and redo logs. You can also add or remove objects in a custom database definition.

### Finalizing Database Creation

After reviewing the Database Summary screen (Figure 9.31), click Finish to start the database creation process. DBCA will create the database, start the instance, and configure all specified options. 

### Configuring an Oracle Database

You can use DBCA to modify an existing database configuration, such as adding options not previously installed or changing the connection mode (Figure 9.8).

### Deleting an Oracle Database

To delete a database, select Delete Database from the DBCA Operations screen. DBCA will list all available databases for deletion and will remove all associated files and services (in Windows) upon confirmation.

### Managing Database Templates

DBCA templates are XML-based files that contain all necessary information for database creation. 

- **Creating Templates**: You can create new templates from existing templates or databases, with or without data (Table 9.10).
- **Deleting Templates**: Use DBCA to remove existing templates from the system.

This concludes the use of DBCA for creating, configuring, and managing Oracle 12c databases.

# Working with Oracle Database Metadata

Oracle databases contain not only user data but also system tables that store metadata—data about the database itself. This metadata includes information such as the names and structures of database objects, security details, and real-time performance metrics. As a DBA, understanding and utilizing this metadata is essential for efficient database management.

## Types of Metadata Views in Oracle Database 12c

Oracle Database 12c provides two primary types of metadata views:
1. **Data Dictionary Views**
2. **Dynamic Performance Views**

These views are owned by the `SYS` user and stored in the `SYSTEM` tablespace.

### Data Dictionary Views

Data dictionary views provide static information about the database and its objects. These views are categorized into:
- **DBA_ Views**: Show information about all database objects, available only to users with DBA privileges.
- **ALL_ Views**: Show information about objects accessible to the current user.
- **USER_ Views**: Show information about objects owned by the current user.
- **CDB_ Views**: Specific to container databases (CDB), these views include a container identifier to provide information across multiple pluggable databases (PDBs).

#### Examples of Data Dictionary Views

| Dictionary View   | Description |
|-------------------|-------------|
| DBA_TABLES        | Shows names and physical storage information about all tables in the database. |
| DBA_USERS         | Provides details about all users in the database. |
| DBA_VIEWS         | Lists information about all views in the database. |
| DBA_TAB_COLUMNS   | Displays column names and data types for tables in the database. |
| DBA_TABLESPACES   | Offers information on all tablespaces within the database. |
| DBA_DATA_FILES    | Details the data files associated with the database. |

Data dictionary views are typically used by DBAs for a broad perspective on the database's metadata.

### Dynamic Performance Views

Dynamic performance views, also known as fixed views, provide real-time information about the database's operation and performance. These views are created on top of dynamic performance tables, which Oracle updates constantly to reflect current database activity.

- **X$**: The base tables for dynamic performance views.
- **V_$**: The views created on the X$ tables.
- **V$**: Public synonyms for the V_$ views, making them easier to access.

#### Examples of Dynamic Performance Views

| Dynamic Performance View | Description |
|--------------------------|-------------|
| V$DATABASE               | Contains metadata about the database, including its name and creation date. |
| V$VERSION                | Displays the software version the database is running. |
| V$OPTION                 | Shows which optional components are installed in the database. |
| V$SQL                    | Provides information about SQL statements executed by database users. |

### Comparing Data Dictionary and Dynamic Performance Views

While both types of views offer metadata, there are key differences between them:

| Aspect                       | Data Dictionary Views       | Dynamic Performance Views       |
|------------------------------|-----------------------------|---------------------------------|
| Naming                       | Usually plural (e.g., DBA_DATA_FILES) | Generally singular (e.g., V$DATAFILE) |
| Availability                 | Available only when the database is open and running | Some are available even when the database is not fully open |
| Data Type                    | Static data that persists across shutdowns | Dynamic data that is reset at database shutdown |
| Usage                        | Used for broader administrative tasks and structural insights | Used for monitoring current database performance and status |

### Scripts for Creating Metadata

The Oracle data dictionary and dynamic performance views are created during database creation. These views are defined by scripts located in the `$ORACLE_HOME/rdbms/admin` directory:
- **catalog.sql**: Creates base dictionary objects.
- **catproc.sql**: Creates PL/SQL packages and functionality.

### Important Notes
- DBAs should not attempt to directly modify data dictionary views or update their information using SQL. The only exception is the `AUD$` table, used for storing database audit information, which can be modified by the `SYS` user.

Understanding and effectively using Oracle's metadata views is crucial for database administration, providing the insight needed to manage and optimize the database environment.


# Managing Initialization-Parameter Files

Oracle uses initialization-parameter files to store information about how an Oracle instance should be configured upon startup. These files play a critical role in determining the instance's behavior and resources. Oracle supports two types of initialization-parameter files: plaintext files (PFILEs) and binary files (SPFILEs).

## PFILEs vs. SPFILEs

PFILEs and SPFILEs serve similar purposes but differ in their formats and capabilities, as summarized in the table below.

| **Pfile** | **Spfile** |
|-----------|------------|
| Text file that can be edited using a text editor. | Binary file that cannot be edited directly. |
| Changes require a restart to take effect. | Parameter changes made with `ALTER SYSTEM` are immediately updated. |
| Named `init<instance_name>.ora`. | Named `spfile<instance_name>.ora`. |
| Instance reads from the pfile only. | Instance reads from and writes to the spfile. |
| Can be created from an spfile using `CREATE PFILE FROM SPFILE`. | Can be created from a pfile using `CREATE SPFILE FROM PFILE`. |

Oracle Database 12c supports over 365 documented configuration parameters, divided into basic and advanced categories. Oracle recommends manually setting only the basic parameters, with others left to default values unless specifically needed.

## Basic Initialization Parameters

The following table describes some of the basic initialization parameters. A "Yes" in the "Static" column indicates that the parameter is static and requires a database restart to take effect.

| **Parameter Name**             | **Static** | **Description** |
|--------------------------------|------------|-----------------|
| CLUSTER_DATABASE               | Yes        | Indicates whether the instance is part of a clustered environment. |
| COMPATIBLE                     | Yes        | Specifies the release level and feature set of the instance. |
| CONTROL_FILES                  | Yes        | Specifies the physical location of the database control files. |
| DB_BLOCK_SIZE                  | Yes        | Specifies the default database block size. |
| DB_CREATE_FILE_DEST            | No         | Specifies the directory for Oracle-Managed Files. |
| DB_CREATE_ONLINE_LOG_DEST_n    | No         | Specifies the locations for redo log files. |
| DB_DOMAIN                      | Yes        | Specifies the logical location of the database on the network. |
| DB_NAME                        | Yes        | Specifies the name of the database mounted by the instance. |
| DB_RECOVERY_FILE_DEST          | No         | Specifies the location for flash recovery files. |
| DB_RECOVERY_FILE_DEST_SIZE     | No         | Specifies the disk space available for flash recovery files. |
| DB_UNIQUE_NAME                 | Yes        | Specifies a globally unique name for the database. |
| INSTANCE_NUMBER                | Yes        | Identifies the instance in a RAC environment. |
| LOG_ARCHIVE_DEST_n             | No         | Specifies up to nine locations for archived redo log files. |
| LOG_ARCHIVE_DEST_STATE_n       | No         | Specifies how to use log archiving locations. |
| NLS_LANGUAGE                   | Yes        | Specifies the default language of the database. |
| NLS_TERRITORY                  | Yes        | Specifies the default region or territory of the database. |
| OPEN_CURSORS                   | No         | Sets the maximum number of open cursors per session. |
| PGA_AGGREGATE_TARGET           | No         | Sets the total memory available for PGA processes. |
| PROCESSES                      | Yes        | Specifies the maximum number of OS processes that can connect to the instance. |
| SESSIONS                       | Yes        | Sets the maximum number of sessions that can connect to the database. |
| SGA_TARGET                     | No         | Sets the maximum size of the SGA. |
| SHARED_SERVERS                 | No         | Specifies the number of shared server processes to start. |
| UNDO_TABLESPACE                | No         | Specifies the tablespace storing undo segments. |

**Note:** Parameters not specified in the pfile or spfile will take on their default values.

### Example PFILE

Below is an example of a typical Oracle Database 12c pfile:

```plaintext
*.audit_file_dest='/u01/app/oracle/admin/c12ndb1/adump'
*.audit_trail='db'
*.compatible='12.1.0.0.0'
*.control_files='/u02/oradata/c12ndb1/control01.ctl','/u01/app/oracle/fast_recovery_area/c12ndb1/control02.ctl'
*.db_block_size=8192
*.db_domain=''
*.db_name='c12ndb1'
*.db_recovery_file_dest='/u01/app/oracle/fast_recovery_area'
*.db_recovery_file_dest_size=11g
*.diagnostic_dest='/u01/app/oracle'
*.dispatchers='(PROTOCOL=TCP) (SERVICE=c12ndb1XDB)'
*.local_listener='LISTENER_C12NDB1'
*.log_archive_format='%t_%s_%r.dbf'
*.memory_target=4000m
*.open_cursors=300
*.processes=300
*.remote_login_passwordfile='EXCLUSIVE'
*.undo_tablespace='UNDOTBS1'
```

## Locating the Default Parameter File

Oracle searches for the parameter file in the following order when a startup command is issued without specifying a pfile or spfile:

1. `spfile$ORACLE_SID.ora`
2. `spfile.ora`
3. `init$ORACLE_SID.ora`

If none of these files are found in the default locations (`$ORACLE_HOME/dbs` on Unix and `%ORACLE_HOME%\database` on Windows), the database will not start.

## Modifying Initialization-Parameter Values

There are three main ways to modify initialization parameters:

1. **Editing the PFILE**: Directly edit the pfile using a text editor. Changes require a database restart.
2. **Using `ALTER SYSTEM` with the SPFILE**: Connect to the instance and make changes using the `ALTER SYSTEM SET parameter_name = value` statement. These changes can take effect immediately or be persistent across restarts, depending on the scope.
3. **Using EM Database Express**: Navigate to the Configuration menu in EM Database Express and choose Initialization Parameters. Changes can be made to the current instance or to the SPFILE for persistence across restarts.

### Using SQL*Plus or SQL Developer

To modify parameters using SQL*Plus or SQL Developer, you can query the `V$PARAMETER` and `V$SPPARAMETER` views to understand the current configuration and make adjustments.

### Querying V$PARAMETER and V$SPPARAMETER

- `V$PARAMETER`: Shows current initialization parameters in effect.
- `V$SPPARAMETER`: Shows parameters in the spfile used to start the instance.

#### Example Query

To see the control file parameters in use:

```sql
SELECT name, value
FROM v$parameter
WHERE name LIKE 'control%'
AND isdefault = 'FALSE';

SELECT name, value
FROM v$spparameter
WHERE name LIKE 'control%'
AND isspecified = 'TRUE';
```

### Using `ALTER SESSION` and `ALTER SYSTEM`

- `ALTER SESSION`: Modifies parameters for the current session only.
- `ALTER SYSTEM`: Modifies parameters at the instance level, with optional scope (MEMORY, SPFILE, BOTH).

#### Example of Modifying a Parameter

To change the `SGA_TARGET` parameter for the current instance and ensure persistence:

```sql
ALTER SYSTEM SET SGA_TARGET=500M SCOPE=BOTH;
```

Use the `SHOW PARAMETER` or `SHOW SPPARAMETER` command to verify the current settings.

In the next section, we will discuss options to start up and shut down an Oracle database.

# Starting up and Shutting down an Oracle Instance

As a DBA, managing the startup and shutdown of an Oracle instance is a critical responsibility. Oracle provides multiple methods to start and stop the database, each suitable for different scenarios. Understanding these options and their appropriate usage is essential, especially for OCA certification exams.

## Privileges for Startup and Shutdown

To start up or shut down an Oracle instance, you need to be connected to the database with appropriate privileges—specifically, SYSDBA or SYSOPER. 

- **SYSDBA**: Allows complete control over the database, including startup, shutdown, and performing all administrative tasks.
- **SYSOPER**: Provides startup and shutdown abilities but restricts access to nonadministrative schema objects.

These authorizations are managed either through a password file or via operating-system control.

## Starting up an Oracle Database 12c Instance

When starting an Oracle database, it transitions through three stages: **NOMOUNT**, **MOUNT**, and **OPEN**. Each stage has specific purposes and usage scenarios.

### STARTUP NOMOUNT
This starts the instance without mounting the database. The parameter file is read, and background processes and memory structures are initialized. However, the instance is not yet associated with the database's physical structures. This mode is typically used for creating a database or rebuilding control files.

**Tip**: If STARTUP NOMOUNT fails, it often indicates that the parameter file cannot be read or is missing, or that there are OS resource limitations.

### STARTUP MOUNT
This mode reads the control file and allows the instance to attach to the physical database structures (data files and redo logs). The database is still not open for user access. Tasks such as enabling or disabling archive logging, renaming data files, and database recovery can be performed in this mode.

### STARTUP OPEN
This is the default startup mode, making the database available for use by all users. It performs the steps of both NOMOUNT and MOUNT modes.

**Other STARTUP Options**:
- **STARTUP OPEN READ ONLY**: Opens the database in read-only mode.
- **STARTUP OPEN RECOVER**: Opens the database and performs recovery.
- **STARTUP FORCE**: Forces a database startup by performing an abort shutdown and then restarting the database. Useful in situations where a normal startup fails.
- **STARTUP RESTRICT**: Opens the database but restricts access to users with the RESTRICTED SESSION privilege. Useful for maintenance tasks.
- **STARTUP UPGRADE/DOWNGRADE**: Used during database version upgrades or downgrades, setting specific initialization parameters required for the process.

## Starting Oracle Using SQL\*Plus

You can use SQL\*Plus to start the Oracle database. Connect as a user with SYSOPER or SYSDBA privileges and use the following syntax:

```sql
STARTUP [NOMOUNT|MOUNT|OPEN] [PFILE=] [RESTRICT] [FORCE] [QUIET]


# Monitoring the Database Alert Log

- **Purpose**: Tracks database activities and errors, essential for diagnosing issues.
- **Contents**:
  - Startup and shutdown logs.
  - Administrative actions (e.g., `ALTER SYSTEM`, `ALTER DATABASE`).
  - Database errors (e.g., ORA-600, ORA-1542).
  - Messages about shared servers, dispatchers, and materialized view refresh errors.
  - Initialization parameters with non-default values.

- **Example Alert Log Excerpt**:
  - Shows startup logs, background processes, and initialization parameters.

- **Log Location**:
  - Controlled by the `DIAGNOSTIC_DEST` parameter.
  - Defaults to `$ORACLE_BASE` or `ORACLE_HOME/rdbms/log` if unset.
  - Alert log files are stored in both text and XML formats under the `trace` and `alert` directories.

- **Dictionary View for Log Location**:
  - Use `V$DIAG_INFO` to find the exact path of the alert log.

- **Maintenance**:
  - Regular purging is recommended.
  - Save a backup of the current log before clearing it.

- **Using ADRCI**:
  - **Command**: `adrci` to interact with the Automatic Diagnostic Repository (ADR).
  - **SHOW ALERT**: View alert logs via ADRCI interface.

# Exercise 9.2: Creating an Oracle Database 12c Database Manually

1. **Set Environment Variables**:
   ```sh
   export ORACLE_SID=OCA12C2
   export ORACLE_BASE=/u01/app/oracle
   export ORACLE_HOME=/u01/app/oracle/product/12.1.0
   ```

2. **Create Password File**:
   ```sh
   orapwd file=orapwOCA12C2
   ```

3. **Create Initialization Parameter File**:
   - Create a pfile and generate an spfile using SQL*Plus:
   ```sh
   sqlplus / as sysdba
   SQL> create spfile from pfile;
   ```

4. **Start Instance in NOMOUNT Mode**:
   ```sql
   SQL> startup nomount;
   ```

5. **Create Database**:
   ```sql
   CREATE DATABASE "c12ndb1"
   DATAFILE '/u02/oradata/c12ndb1/system01.dbf' SIZE 700M REUSE AUTOEXTEND ON
   ...
   ```

6. **Create Additional Tablespaces** (if needed):
   ```sql
   CREATE TABLESPACE "USERS"
   DATAFILE '/u02/oradata/c12ndb1/users01.dbf' SIZE 25M;
   ```

7. **Build Data Dictionary and PL/SQL Packages**:
   ```sql
   SQL> @?/rdbms/admin/catalog.sql
   SQL> @?/rdbms/admin/catproc.sql
   ```

8. **Install Additional Options** (if needed):
   ```sql
   SQL> @?/javavm/install/initjvm.sql;
   ```
# Summary Notes

- **Oracle Database 12c Installation**
  - Installation using Oracle Universal Installer (OUI) and Database Configuration Assistant (DBCA).
  - Requires pre-install checks and meeting hardware requirements.
  - Collaboration between system administrators and DBAs on Unix/Linux platforms for certain script executions.

- **Database Creation with DBCA**
  - Options to use pre-existing XML templates or create custom templates.
  - Defines database aspects: name, file location, sizing, initialization parameters.
  - Capabilities:
    - Create, save, or run database definitions.
    - Remove databases or add options to existing ones.
    - Manage and create new templates centrally.

- **Initialization Parameter Files**
  - Stores instance configuration settings.
  - Two types:
    - **Pfile**: Editable plaintext file.
    - **Spfile**: Binary file, persistent across startups.
  - Use EM Database Express to adjust parameters dynamically.

- **Oracle Metadata Dictionary**
  - Contains information about database objects.
  - Created using `catalog.sql`.
  - Static data in data dictionary views, dynamic data in performance views (not persistent across shutdowns).

- **Database Startup Modes**
  - **MOUNT, NOMOUNT, OPEN**: Different stages of database availability.
  - **RESTRICT**: Limits general access for maintenance.
  - **FORCE**: Shuts down and restarts the database, requires instance recovery.

- **Database Shutdown Options**
  - **NORMAL**: Waits for all users to disconnect.
  - **TRANSACTIONAL**: Waits for all active transactions to complete.
  - **IMMEDIATE**: Rolls back uncommitted transactions, disconnects users.
  - **ABORT**: Immediate shutdown, no rollback, requires instance recovery.

- **Database Alert Log**
  - Tracks database activities and errors, crucial for diagnostics.
  - Default location determined by `DIAGNOSTIC_DEST`.
  - Contains startup/shutdown info, administrative actions, errors, etc.
  - Regular purging recommended to manage log size.
