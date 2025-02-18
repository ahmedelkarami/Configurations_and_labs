**"Oracle Database Versions: A Technical Reference Guide for DBAs."** 
This chapter focuses on **Oracle Database 18c and 19c**, which introduced features like **automatic indexing**, **real-time statistics**, and **SQL quarantine**. It covers the technical aspects of these features, their benefits, and hands-on implementation.

---

# **Chapter 5: Oracle Database 18c and 19c - Stability and Automation**

---

## **5.1 Overview of Oracle Database 18c and 19c**

Oracle Database 18c and 19c continued the trend of automation and stability, building on the foundation laid by Oracle Database 12c. Oracle Database 19c, in particular, is a **Long-Term Support (LTS)** release, making it a preferred choice for production environments. These versions introduced features like **automatic indexing**, **real-time statistics**, and **SQL quarantine**, which further simplified database administration and improved performance.

---

## **5.2 Key Features of Oracle Database 18c and 19c**

### **5.2.1 Automatic Indexing**
- **Purpose:** Automatically creates, drops, and rebuilds indexes based on workload patterns.
- **How It Works:**
  - The **Automatic Indexing** feature monitors SQL workloads and identifies opportunities for new indexes.
  - It also drops unused or redundant indexes.
- **Benefits:**
  - Reduces the need for manual index tuning.
  - Improves query performance by ensuring optimal indexing.

### **5.2.2 Real-Time Statistics**
- **Purpose:** Collects optimizer statistics in real-time during data changes.
- **How It Works:**
  - Statistics are updated automatically as data is inserted, updated, or deleted.
  - Eliminates the need for manual statistics gathering.
- **Benefits:**
  - Ensures accurate and up-to-date statistics for the optimizer.
  - Improves query performance by avoiding stale statistics.

### **5.2.3 SQL Quarantine**
- **Purpose:** Prevents problematic SQL statements from executing repeatedly.
- **How It Works:**
  - When a SQL statement causes a severe performance issue (e.g., excessive resource usage), it is quarantined.
  - Future executions of the quarantined SQL are blocked.
- **Benefits:**
  - Protects the database from runaway queries.
  - Reduces the impact of poorly performing SQL.

### **5.2.4 Other Notable Features**
- **Active Data Guard DML Redirection:**
  - Allows read-only standby databases to execute DML operations by redirecting them to the primary database.
- **Polymorphic Table Functions:**
  - Enables table functions to return different result sets based on input parameters.
- **Automatic Materialized Views:**
  - Automatically creates and refreshes materialized views based on query patterns.

---

## **5.3 Hands-On: Implementing Automatic Indexing**

### **5.3.1 Enabling Automatic Indexing**
1. **Enable Automatic Indexing:**
   ```sql
   EXEC DBMS_AUTO_INDEX.CONFIGURE('AUTO_INDEX_MODE', 'IMPLEMENT');
   ```

2. **Verify Automatic Indexing Configuration:**
   ```sql
   SELECT parameter_name, parameter_value
   FROM dba_auto_index_config;
   ```

### **5.3.2 Monitoring Automatic Indexing**
1. **View Automatic Indexing Reports:**
   ```sql
   SELECT dbms_auto_index.report_activity() FROM dual;
   ```

2. **Check Created Indexes:**
   ```sql
   SELECT index_name, table_name, auto
   FROM dba_indexes
   WHERE auto = 'YES';
   ```

---

## **5.4 Hands-On: Using Real-Time Statistics**

### **5.4.1 Enabling Real-Time Statistics**
1. **Set the OPTIMIZER_REAL_TIME_STATISTICS Parameter:**
   ```sql
   ALTER SYSTEM SET OPTIMIZER_REAL_TIME_STATISTICS = TRUE;
   ```

2. **Verify Real-Time Statistics:**
   ```sql
   SELECT table_name, last_analyzed
   FROM user_tables
   WHERE table_name = 'SALES';
   ```

### **5.4.2 Testing Real-Time Statistics**
1. **Insert Data into a Table:**
   ```sql
   INSERT INTO sales (sale_id, sale_date, amount)
   VALUES (1, SYSDATE, 1000);
   ```

2. **Check Statistics:**
   ```sql
   SELECT num_rows, last_analyzed
   FROM user_tables
   WHERE table_name = 'SALES';
   ```

---

## **5.5 Hands-On: Using SQL Quarantine**

### **5.5.1 Enabling SQL Quarantine**
1. **Set the SQL_QUARANTINE Parameter:**
   ```sql
   ALTER SYSTEM SET SQL_QUARANTINE = 'ON';
   ```

2. **Verify SQL Quarantine Configuration:**
   ```sql
   SELECT name, value
   FROM v$parameter
   WHERE name = 'sql_quarantine';
   ```

### **5.5.2 Testing SQL Quarantine**
1. **Run a Problematic Query:**
   ```sql
   SELECT * FROM sales WHERE sale_date = '2023-01-01';
   ```

2. **Check Quarantined SQL:**
   ```sql
   SELECT sql_id, sql_text, quarantined
   FROM v$sql
   WHERE quarantined = 'YES';
   ```

---

## **5.6 Summary of Oracle Database 18c and 19c Features**

| **Feature**                     | **Description**                                                                 |
|----------------------------------|---------------------------------------------------------------------------------|
| **Automatic Indexing**           | Automatically creates, drops, and rebuilds indexes based on workload patterns.  |
| **Real-Time Statistics**         | Collects optimizer statistics in real-time during data changes.                 |
| **SQL Quarantine**               | Prevents problematic SQL statements from executing repeatedly.                  |
| **Active Data Guard DML Redirection** | Allows read-only standby databases to execute DML operations.              |
| **Polymorphic Table Functions**  | Enables table functions to return different result sets based on input parameters. |
| **Automatic Materialized Views** | Automatically creates and refreshes materialized views based on query patterns. |

---

## **5.7 Key Takeaways**
- Oracle Database 18c and 19c introduced features like **automatic indexing**, **real-time statistics**, and **SQL quarantine**, which further simplified database administration and improved performance.
- **Automatic Indexing** reduces the need for manual index tuning.
- **Real-Time Statistics** ensures accurate and up-to-date statistics for the optimizer.
- **SQL Quarantine** protects the database from runaway queries.
- Hands-on implementation of these features is essential for DBAs to maximize their benefits in modern environments.

---
