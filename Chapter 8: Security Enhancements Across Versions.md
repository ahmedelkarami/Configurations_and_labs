**"Oracle Database Versions: A Technical Reference Guide for DBAs."** 
This chapter focuses on **security enhancements across Oracle Database versions**, covering features like **data redaction**, **unified auditing**, and **SQL Firewall**. It includes technical details, benefits, and hands-on implementation.

---

# **Chapter 8: Security Enhancements Across Versions**

---

## **8.1 Overview of Security Enhancements**

Security is a critical aspect of database administration, and Oracle Database has introduced numerous features over the years to protect data and ensure compliance with regulatory requirements. This chapter explores the evolution of security features across Oracle Database versions, focusing on **data redaction**, **unified auditing**, and **SQL Firewall**.

---

## **8.2 Data Redaction and Encryption**

### **8.2.1 Data Redaction**
- **Purpose:** Masks sensitive data in query results based on user roles.
- **How It Works:**
  - Data is redacted at runtime, ensuring that only authorized users see the actual data.
  - Supports partial, full, and random redaction.
- **Benefits:**
  - Protects sensitive data from unauthorized access.
  - Ensures compliance with data privacy regulations.

### **8.2.2 Transparent Data Encryption (TDE)**
- **Purpose:** Encrypts data at rest to protect it from unauthorized access.
- **How It Works:**
  - Data is encrypted before being written to disk and decrypted when read.
  - Supports encryption of tablespaces, columns, and backups.
- **Benefits:**
  - Ensures data security without requiring changes to applications.
  - Simplifies compliance with data protection regulations.

---

## **8.3 Unified Auditing**

### **8.3.1 Purpose**
- **Purpose:** Provides a centralized and consistent way to audit database activities.
- **How It Works:**
  - Auditing data is stored in a unified audit trail, making it easier to manage and analyze.
  - Supports fine-grained auditing (FGA) and standard auditing.
- **Benefits:**
  - Simplifies audit management and reporting.
  - Ensures compliance with regulatory requirements.

### **8.3.2 Enabling Unified Auditing**
1. **Enable Unified Auditing:**
   ```sql
   ALTER SYSTEM SET audit_trail=DB, EXTENDED SCOPE=SPFILE;
   ```

2. **Restart the Database:**
   ```sql
   SHUTDOWN IMMEDIATE;
   STARTUP;
   ```

### **8.3.3 Creating Audit Policies**
1. **Create an Audit Policy:**
   ```sql
   CREATE AUDIT POLICY audit_sales_access
   ACTIONS SELECT, INSERT, UPDATE, DELETE
   ON sales;
   ```

2. **Enable the Audit Policy:**
   ```sql
   AUDIT POLICY audit_sales_access;
   ```

### **8.3.4 Viewing Audit Data**
1. **Query the Unified Audit Trail:**
   ```sql
   SELECT dbusername, action_name, object_name, sql_text
   FROM unified_audit_trail
   WHERE object_name = 'SALES';
   ```

---

## **8.4 SQL Firewall**

### **8.4.1 Purpose**
- **Purpose:** Protects against SQL injection attacks by monitoring and blocking malicious SQL statements.
- **How It Works:**
  - Monitors SQL statements executed against the database.
  - Blocks statements that match predefined rules or patterns.
- **Benefits:**
  - Enhances database security by preventing SQL injection attacks.
  - Simplifies compliance with security standards.

### **8.4.2 Enabling SQL Firewall**
1. **Enable SQL Firewall:**
   ```sql
   ALTER SYSTEM SET sql_firewall = ON;
   ```

2. **Verify SQL Firewall Configuration:**
   ```sql
   SELECT name, value
   FROM v$parameter
   WHERE name = 'sql_firewall';
   ```

### **8.4.3 Testing SQL Firewall**
1. **Run a Malicious Query:**
   ```sql
   SELECT * FROM sales WHERE sale_id = '1 OR 1=1';
   ```

2. **Check Blocked Queries:**
   ```sql
   SELECT sql_text, blocked
   FROM v$sql_firewall
   WHERE blocked = 'YES';
   ```

---

## **8.5 Hands-On: Implementing Data Redaction**

### **8.5.1 Creating a Data Redaction Policy**
1. **Create a Data Redaction Policy:**
   ```sql
   BEGIN
       DBMS_REDACT.ADD_POLICY(
           object_schema => 'HR',
           object_name => 'EMPLOYEES',
           column_name => 'SALARY',
           policy_name => 'REDACT_SALARY',
           function_type => DBMS_REDACT.PARTIAL,
           function_parameters => 'VVVF'
       );
   END;
   ```

2. **Verify the Redaction Policy:**
   ```sql
   SELECT object_name, column_name, policy_name
   FROM redaction_policies;
   ```

### **8.5.2 Testing Data Redaction**
1. **Query the Redacted Data:**
   ```sql
   SELECT salary FROM hr.employees;
   ```

2. **Check Redacted Results:**
   - The salary column should display redacted values (e.g., 'VVVF').

---

## **8.6 Hands-On: Using Transparent Data Encryption (TDE)**

### **8.6.1 Enabling TDE**
1. **Set the Encryption Key:**
   ```sql
   ADMINISTER KEY MANAGEMENT SET KEY
   IDENTIFIED BY password;
   ```

2. **Encrypt a Tablespace:**
   ```sql
   ALTER TABLESPACE users ENCRYPTION ONLINE USING 'AES256';
   ```

3. **Verify Encryption:**
   ```sql
   SELECT tablespace_name, encrypted
   FROM dba_tablespaces;
   ```

---

## **8.7 Summary of Security Enhancements**

| **Feature**                     | **Description**                                                                 |
|----------------------------------|---------------------------------------------------------------------------------|
| **Data Redaction**               | Masks sensitive data in query results based on user roles.                      |
| **Transparent Data Encryption (TDE)** | Encrypts data at rest to protect it from unauthorized access.               |
| **Unified Auditing**             | Provides a centralized and consistent way to audit database activities.         |
| **SQL Firewall**                 | Protects against SQL injection attacks by monitoring and blocking malicious SQL statements. |

---

## **8.8 Key Takeaways**
- Oracle Database has introduced numerous security features to protect data and ensure compliance with regulatory requirements.
- **Data Redaction** and **Transparent Data Encryption (TDE)** protect sensitive data from unauthorized access.
- **Unified Auditing** simplifies audit management and reporting.
- **SQL Firewall** enhances database security by preventing SQL injection attacks.
- Hands-on implementation of these features is essential for maximizing their benefits in modern environments.

---
