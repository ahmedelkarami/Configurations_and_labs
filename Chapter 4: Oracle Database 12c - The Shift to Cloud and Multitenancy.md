This chapter focuses on **Oracle Database 12c**, which introduced groundbreaking features like **multitenant architecture**, **In-Memory Column Store**, and **Adaptive Query Optimization**. It covers the technical aspects of these features, their benefits, and hands-on implementation.

---

# **Chapter 4: Oracle Database 12c - The Shift to Cloud and Multitenancy**

---

## **4.1 Overview of Oracle Database 12c**

Oracle Database 12c, released in 2013, marked a significant shift in Oracle's strategy toward cloud computing and database consolidation. The introduction of the **multitenant architecture** revolutionized how databases are managed, making it easier to consolidate multiple databases into a single container. Other key features like the **In-Memory Column Store** and **Adaptive Query Optimization** further enhanced performance and scalability.

---

## **4.2 Key Features of Oracle Database 12c**

### **4.2.1 Multitenant Architecture**
- **Purpose:** Simplifies database consolidation by allowing multiple pluggable databases (PDBs) to run within a single container database (CDB).
- **Components:**
  - **Container Database (CDB):** A single database instance that hosts multiple PDBs.
  - **Pluggable Database (PDB):** A portable database that can be plugged into a CDB.
- **Benefits:**
  - Reduces overhead by sharing resources (e.g., memory, background processes) across PDBs.
  - Simplifies database management and patching.
  - Enables rapid provisioning of new databases.

### **4.2.2 In-Memory Column Store**
- **Purpose:** Improves query performance for analytical workloads by storing data in memory in a columnar format.
- **How It Works:**
  - Data is stored in both row format (for OLTP) and column format (for analytics).
  - Queries on large datasets are significantly faster.
- **Benefits:**
  - Accelerates reporting and analytics.
  - Reduces the need for additional indexing.

### **4.2.3 Adaptive Query Optimization**
- **Purpose:** Enhances query performance by adapting execution plans based on runtime statistics.
- **Components:**
  - **Adaptive Plans:** Dynamically adjusts join methods and distribution methods during query execution.
  - **Adaptive Statistics:** Automatically gathers additional statistics for complex queries.
- **Benefits:**
  - Improves query performance without manual tuning.
  - Reduces the risk of suboptimal execution plans.

### **4.2.4 Other Notable Features**
- **SQL Pattern Matching:**
  - Allows complex pattern matching in SQL using the `MATCH_RECOGNIZE` clause.
- **JSON Support:**
  - Enables storage and querying of JSON data using SQL.
- **Data Redaction:**
  - Masks sensitive data in query results based on user roles.

---

## **4.3 Hands-On: Creating and Managing Pluggable Databases (PDBs)**

### **4.3.1 Creating a Container Database (CDB)**
1. **Create a CDB:**
   ```sql
   CREATE DATABASE cdb1
   USER SYS IDENTIFIED BY password
   USER SYSTEM IDENTIFIED BY password
   ENABLE PLUGGABLE DATABASE
   SEED FILE_NAME_CONVERT=('/u01/app/oracle/oradata/cdb1/pdbseed/', '/u01/app/oracle/oradata/cdb1/pdb1/');
   ```

2. **Verify the CDB:**
   ```sql
   SELECT name, cdb FROM v$database;
   ```

### **4.3.2 Creating a Pluggable Database (PDB)**
1. **Create a PDB:**
   ```sql
   CREATE PLUGGABLE DATABASE pdb1
   ADMIN USER pdbadmin IDENTIFIED BY password
   FILE_NAME_CONVERT=('/u01/app/oracle/oradata/cdb1/pdbseed/', '/u01/app/oracle/oradata/cdb1/pdb1/');
   ```

2. **Open the PDB:**
   ```sql
   ALTER PLUGGABLE DATABASE pdb1 OPEN;
   ```

3. **Verify the PDB:**
   ```sql
   SELECT name, open_mode FROM v$pdbs;
   ```

### **4.3.3 Cloning a PDB**
1. **Clone a PDB:**
   ```sql
   CREATE PLUGGABLE DATABASE pdb2 FROM pdb1
   FILE_NAME_CONVERT=('/u01/app/oracle/oradata/cdb1/pdb1/', '/u01/app/oracle/oradata/cdb1/pdb2/');
   ```

2. **Open the Cloned PDB:**
   ```sql
   ALTER PLUGGABLE DATABASE pdb2 OPEN;
   ```

---

## **4.4 Hands-On: Using the In-Memory Column Store**

### **4.4.1 Enabling the In-Memory Column Store**
1. **Set the INMEMORY_SIZE Parameter:**
   ```sql
   ALTER SYSTEM SET INMEMORY_SIZE = 1G SCOPE=SPFILE;
   ```

2. **Restart the Database:**
   ```sql
   SHUTDOWN IMMEDIATE;
   STARTUP;
   ```

### **4.4.2 Enabling In-Memory for a Table**
1. **Enable In-Memory for a Table:**
   ```sql
   ALTER TABLE sales INMEMORY;
   ```

2. **Verify In-Memory Status:**
   ```sql
   SELECT table_name, inmemory_compression, inmemory_priority
   FROM user_tables
   WHERE table_name = 'SALES';
   ```

### **4.4.3 Querying In-Memory Data**
1. **Run a Query:**
   ```sql
   SELECT * FROM sales WHERE sale_date = '2023-01-01';
   ```

2. **Check In-Memory Statistics:**
   ```sql
   SELECT * FROM v$inmemory_area;
   ```

---

## **4.5 Hands-On: Using Adaptive Query Optimization**

### **4.5.1 Enabling Adaptive Query Optimization**
1. **Set the OPTIMIZER_ADAPTIVE_PLANS Parameter:**
   ```sql
   ALTER SYSTEM SET OPTIMIZER_ADAPTIVE_PLANS = TRUE;
   ```

2. **Set the OPTIMIZER_ADAPTIVE_STATISTICS Parameter:**
   ```sql
   ALTER SYSTEM SET OPTIMIZER_ADAPTIVE_STATISTICS = TRUE;
   ```

### **4.5.2 Testing Adaptive Plans**
1. **Run a Query:**
   ```sql
   SELECT * FROM sales s JOIN customers c ON s.customer_id = c.customer_id;
   ```

2. **Check the Execution Plan:**
   ```sql
   SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR);
   ```

---

## **4.6 Summary of Oracle Database 12c Features**

| **Feature**                     | **Description**                                                                 |
|----------------------------------|---------------------------------------------------------------------------------|
| **Multitenant Architecture**     | Simplifies database consolidation using CDBs and PDBs.                         |
| **In-Memory Column Store**       | Improves query performance for analytical workloads.                           |
| **Adaptive Query Optimization**  | Enhances query performance by adapting execution plans.                        |
| **SQL Pattern Matching**         | Allows complex pattern matching in SQL.                                        |
| **JSON Support**                 | Enables storage and querying of JSON data.                                     |
| **Data Redaction**               | Masks sensitive data in query results.                                         |

---

## **4.7 Key Takeaways**
- Oracle Database 12c introduced **multitenant architecture**, revolutionizing database consolidation and management.
- The **In-Memory Column Store** significantly improved performance for analytical workloads.
- **Adaptive Query Optimization** reduced the need for manual query tuning.
- Hands-on implementation of these features is essential for DBAs to maximize their benefits in modern environments.

---
