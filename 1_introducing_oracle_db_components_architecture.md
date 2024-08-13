# Chapter 8: Introducing Oracle Database 12c Components and Architecture

## Oracle Database 12c: OCA Exam Objectives

### Key Areas Covered:
- **Oracle Database architecture components.**
- **Memory structures in Oracle Database.**
- **Background processes in Oracle Database.**
- **Relationship between logical and physical storage structures.**
- **Usage of database management tools.**

## Chapter Overview
### Purpose:
- This chapter introduces Oracle Database 12c administration fundamentals and lays the groundwork for the Oracle Database 12c: Installation and Administration OCA certification exam.

### Exam Structure:
- The exam is divided into two main parts:
  1. **Database Administration:** Managing and maintaining Oracle Database 12c.
  2. **Installation, Upgrading, and Patching:** Procedures for installing and maintaining the database.

### Oracle 12c Database Overview:
- **Features:** Performance, availability, recoverability, multitenancy, cloud-enabled, application-testing, and security.
- **Role of DBA:** Manage the Oracle Database 12c environment throughout its lifecycle, from installation to daily administration.
- **Knowledge Requirements:** Understanding Oracle’s architecture, relational database concepts, and database management tools.

## Key Topics Discussed
1. **Oracle Database Architecture:**
   - Overview of Oracle Database 12c architecture, including memory structures, background processes, and data storage methods.
   - Importance of understanding these components for effective database administration.

2. **Database Management Tools:**
   - Tools used to monitor and manage Oracle Database 12c.

3. **Learning Approach:**
   - **Initial Focus:** Understanding Oracle architecture basics before moving to database creation.
   - **Next Steps:** Practical database creation will be covered in the following chapter.

## Important Note
- **Exam Objectives Flexibility:** Oracle may update exam objectives without notice. Always check Oracle's Training and Certification website for the most current information.

# Oracle Database Fundamentals

## Introduction to Databases and DBMS
- **Databases** store related logical units of information.
- **Database Management System (DBMS):** Facilitates storage, modification, and retrieval of data.
- **Historical Context:**
  - Early databases used flat files or hierarchical structures.
  - Early DBMSs mixed physical and logical data manipulation.
- **Relational DBMS (RDBMS):**
  - Introduced data independence, separating physical and logical data models.
  - Oracle is a relational DBMS, influenced by Dr. Edgar Codd’s relational model (1970).

## Relational Databases
- **Concept:**
  - Data is stored in relational objects, mainly tables.
  - Tables store data in rows and columns, with relationships defined by keys.
- **Primary Key:**
  - Uniquely identifies rows in a table.
  - Each table must have a primary key.
- **Foreign Key:**
  - Establishes relationships between tables by referencing a primary key in another table.
  - Defines parent-child relationships between tables, enforced by Oracle using constraints.

## Oracle Database 12c Objects
- **Supported Objects:**
  - **Table:** Basic storage form, consisting of rows and columns.
  - **View:** Stored query, no data storage.
  - **Index:** Structure to enhance data retrieval speed.
  - **Materialized View:** Stores summarized data, unlike a regular view.
  - **Index-Organized Table:** Stores data alongside index for efficiency.
  - **Cluster:** Groups tables sharing common columns.
  - **Constraint:** Enforces data integrity.
  - **Sequence:** Generates continuous numbers.
  - **Synonym:** Alias for database schema objects.
  - **Trigger:** Executes PL/SQL code in response to events.
  - **Stored Function/Procedure:** PL/SQL programs for user-defined functions or business processes.
  - **Package:** Collection of PL/SQL procedures and functions.
  - **Java:** Java procedures for business logic.
  - **Database Link:** Allows communication between databases.

## Interacting with Oracle Database 12c
- **SQL (Structured Query Language):**
  - Language used to interact with Oracle Database 12c for creating objects and managing data.
- **Database Management Tools:**
  - **SQL*Plus:** Command-line interface for executing SQL and managing the database.
  - **SQL Developer:** GUI tool for database development, object management, and PL/SQL programming.
  - **Oracle Enterprise Manager Database Express 12c:**
    - Web-based management tool bundled with Oracle Database 12c.
    - Manages a single database; requires the database to be open for usage.

## Tools Overview
1. **SQL*Plus:**
   - Primary tool for Oracle DBAs to administer databases.
   - Accessible via command prompt or terminal.

2. **SQL Developer:**
   - GUI tool for database development, object manipulation, and SQL execution.
   - Includes utilities for migrating databases from other platforms to Oracle.

3. **Enterprise Manager Database Express 12c:**
   - Web-based graphical tool for single database management.
   - Requires XMLDB to be installed and configured during database creation.

## Note on Oracle Enterprise Manager (OEM) Cloud Control
- OEM Cloud Control is a separate installation for managing multiple databases and other Oracle and non-Oracle services.
- **Learn More:** Visit the Oracle website for further details on OEM Cloud Control.

## Next Steps
- In the next section, you’ll learn about Oracle 12c architecture, building on the fundamentals covered here.

# Oracle Database 12c Architecture

## Overview
- **User Interaction:** Tools for database interaction require user accounts, network connectivity, storage capacity, and recovery mechanisms.
- **DBA Responsibilities:**
  - Selecting server hardware.
  - Installing and configuring Oracle Database 12c.
  - Deciding between Container Database or traditional single database.
  - Creating and managing databases, tables, objects, and users.
  - Establishing backup and recovery procedures.
  - Monitoring and tuning database performance.
  - Analyzing trends for resource and storage requirements.

## Oracle Server Architecture
- **Three Categories:**
  1. **Server Processes:** Communicate with user processes and interact with an Oracle instance.
  2. **Logical Memory Structures:** Collectively called an Oracle instance.
  3. **Physical File Structures:** Collectively called a database.
- **Instance vs. Database:**
  - **Instance:** Composed of memory structures and background processes.
  - **Database:** Physical files that store data.
  - **Real Application Clusters (RAC):** Multiple instances accessing a single database (not covered in OCA exam).

## Key Oracle Components
- **Memory Structures:** Process and memory structures together form an instance.
- **Storage Structures:** Collectively called a database.
- **Instance + Database = Oracle Server.**

## Schemas and Users
- **Schema:** Collection of database objects like tables, indexes, and views associated with a user.
- **User:** Defined database entity with rights to perform activities.
- **Schema vs. User:** Users perform work; schemas are collections of objects on which users work.

## User and Server Processes
- **User Process:** Supports user’s connection to the instance.
- **Server Process:** Responsible for actual interaction with the database on behalf of the user.
- **Program Global Area (PGA):** Memory structure created for each server process, storing user-specific session information.

## Oracle Instance
- **System Global Area (SGA):** Oracle’s main memory structure.
- **Components of SGA:**
  - **Shared Pool:** Caches SQL statements.
  - **Database Buffer Cache:** Caches recently accessed data.
  - **Redo Log Buffer:** Stores transaction information for recovery.

## Optional SGA Components
- **Java Pool:** Caches Java objects and application code.
- **Large Pool:** Caches data for large operations like RMAN backup.
- **Streams Pool:** Caches data for queued message requests.
- **Result Cache:** Stores results of SQL queries and PL/SQL functions.

## Automatic Memory Management (AMM)
- **Memory Management:** Oracle Database 12c can automatically manage SGA and PGA components using AMM.
- **Granules:** Memory in SGA is allocated in units called granules.

## Oracle Background Processes
- **Required Background Processes:**
  - **DBWn (Database Writer):** Writes modified database blocks to data files.
  - **CKPT (Checkpoint):** Updates data file headers following a checkpoint event.
  - **LGWR (Log Writer):** Writes transaction recovery information to redo log files.
  - **PMON (Process Monitor):** Cleans up failed user database connections.
  - **SMON (System Monitor):** Performs instance recovery and manages space used for sorting.

- **Optional Background Processes:**
  - **ARCn (Archiver):** Copies redo log files to the archive location.
  - **MMAN (Memory Manager):** Manages SGA component sizes when AMM is used.

## Oracle Storage Structures
- **Control Files:** Store crucial database information like database name, file locations, and recovery information.
- **Data Files:** Store the actual data within the database; organized into tablespaces.
- **Redo Log Files:** Record changes made to the database, used for recovery.

## Real Application Clusters (RAC)
- **RAC Overview:** Allows multiple Oracle instances to run on multiple nodes, accessing a single database.
- **Shared Components:** Control files, data files.
- **Non-Shared Components:** Undo tablespace, redo log files.

## Logical Structure
- **Tablespaces:** Logical division of the database, grouping related logical structures together.
- **Blocks:** Smallest unit of storage in Oracle, based on `DB_BLOCK_SIZE`.
- **Extents:** Grouping of contiguous blocks.
- **Segments:** Set of extents allocated for logical structures like tables and indexes.

## Data Dictionary for Physical and Logical Structures
- **Physical Storage Structures:**
  - Control Files: `V$CONTROLFILE`
  - Redo Log Files: `V$LOG`, `V$LOGFILE`
  - Data Files: `V$DATAFILE`, `V$TEMPFILE`, `DBA_DATA_FILES`, `DBA_TEMP_FILES`
  
- **Logical Storage Structures:**
  - Tablespaces: `DBA_TABLESPACES`
  - Segments: `DBA_SEGMENTS`
  - Extents: `DBA_EXTENTS`

## Real-World Scenario
- **Exploring Data Dictionary:** Use views like `V$` and `DBA` to explore the physical and logical structures of your database.

## Important Figures
- **Figure 8.5:** Oracle Database 12c Architecture.
- **Figure 8.6:** Oracle Database 12c Multitenancy.
- **Figure 8.7:** Relationship Between User and Server Processes and the PGA.
- **Figure 8.8:** Components of the SGA.
- **Figure 8.9:** EM Database Express Showing SGA Components.
- **Figure 8.10:** The OEM Database Express Storage Menu.
- **Figure 8.11:** The SQL Developer DBA Menu.
- **Figure 8.12:** EM Database Express Showing Control Files.
- **Figure 8.13:** EM Database Express Showing Data Files.
- **Figure 8.14:** EM Database Express Showing Redo Logs.
- **Figure 8.15:** How ARCn Copies Redo Log Entries to Disk.
- **Figure 8.16:** The SQL Developer Screen Showing Database Storage.
- **Figure 8.17:** Logical Database Structure.

# Summary

This chapter introduced the Oracle Database 12c architecture and the components that make up an Oracle database server. 

## Key Concepts:

- **Relational Databases:** Oracle is a relational database where data is stored in tables consisting of rows and columns. SQL is the language used for managing and administering Oracle databases.

- **Administration Tools:**
  - **SQL*Plus:** A command-line tool used by DBAs.
  - **Oracle Enterprise Manager:** A GUI tool for database management.
  - **SQL Developer:** A GUI tool with DBA functions, offering a user-friendly interface for interacting with Oracle Database 12c.

## Oracle Database 12c Architecture:

- **Major Components:**
  1. **Memory:** Managed through structures like the system global area (SGA), which includes the shared pool, database buffer cache, and redo log buffer.
  2. **Processes:** Includes background processes that manage the database instance, like database writer (DBWn), checkpoint writer (CKPT), log writer (LGWR), process monitor (PMON), and system monitor (SMON).
  3. **Storage:** Physical files stored on disk, such as control files, data files, and redo log files.

- **Process Flow:**
  - A user process initiates a connection and starts a server process, which interacts with the SGA and performs tasks on the database.

## Memory Structures:

- **SGA Components:**
  - **Shared Pool**
  - **Database Buffer Cache**
  - **Redo Log Buffer**
  - **Optional Pools:** Java pool, large pool, result cache, and streams pool.

## Background Processes:

- **Essential Processes:** DBWn, CKPT, LGWR, PMON, and SMON.
- **Additional Processes:** Depending on the configuration, processes like Archiver (ARCn) and ASM balancing may also be present.

## Physical Data Structure:

- **Control Files:** Store vital information like database names, file locations, and backup details. The CKPT process updates the control file.
- **Redo Log Files:** Contain information for recovery, written by the LGWR process.
- **Data Files:** Store Oracle metadata and application data, with DBWn managing the writing of dirty blocks from the buffer cache to these files.

## Logical Structure:

- **Hierarchy:**
  - **Tablespace:** The highest logical unit, containing segments.
  - **Segments:** Comprise one or more extents.
  - **Extent:** A contiguous allocation of blocks.
  - **Block:** The smallest unit of storage within the Oracle database.
