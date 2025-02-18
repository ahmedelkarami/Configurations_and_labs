**"Oracle Database Versions: A Technical Reference Guide for DBAs."** 
This chapter focuses on **Oracle Database 21c and 23c**, which introduced cutting-edge features like **native JSON datatype**, **blockchain tables**, and **JSON Relational Duality**. It covers the technical aspects of these features, their benefits, and hands-on implementation.

---

# **Chapter 6: Oracle Database 21c and 23c - Modern Innovations**

---

## **6.1 Overview of Oracle Database 21c and 23c**

Oracle Database 21c and 23c represent the latest innovations in Oracle's database technology. Oracle Database 21c, released in 2020, was an **Innovation Release**, while Oracle Database 23c, released in 2023, is a **Long-Term Support (LTS)** release. These versions introduced features like **native JSON datatype**, **blockchain tables**, and **JSON Relational Duality**, which cater to modern application development and data management needs.

---

## **6.2 Key Features of Oracle Database 21c and 23c**

### **6.2.1 Native JSON Datatype**
- **Purpose:** Provides native support for storing and querying JSON data.
- **How It Works:**
  - JSON data is stored in a binary format for efficient storage and retrieval.
  - Supports JSON functions and operators for querying and manipulating JSON data.
- **Benefits:**
  - Simplifies working with semi-structured data.
  - Improves performance for JSON operations.

### **6.2.2 Blockchain Tables**
- **Purpose:** Provides tamper-proof data storage for applications requiring high data integrity.
- **How It Works:**
  - Data in blockchain tables is cryptographically chained, making it immutable.
  - Only append operations are allowed; updates and deletes are prohibited.
- **Benefits:**
  - Ensures data integrity and auditability.
  - Ideal for applications like financial transactions and supply chain tracking.

### **6.2.3 JSON Relational Duality**
- **Purpose:** Combines the benefits of relational and JSON data models.
- **How It Works:**
  - Allows developers to work with the same data using both relational and JSON interfaces.
  - Changes made in one model are automatically reflected in the other.
- **Benefits:**
  - Simplifies application development by providing flexibility in data modeling.
  - Enhances performance for both transactional and analytical workloads.

### **6.2.4 Other Notable Features**
- **AutoML for In-Database Machine Learning:**
  - Automates the process of building and deploying machine learning models within the database.
- **SQL Firewall:**
  - Protects against SQL injection attacks by monitoring and blocking malicious SQL statements.
- **Enhanced Sharding:**
  - Improves scalability and performance for distributed databases.

---

## **6.3 Hands-On: Using the Native JSON Datatype**

### **6.3.1 Creating a Table with JSON Datatype**
1. **Create a Table:**
   ```sql
   CREATE TABLE customer_data (
       id NUMBER PRIMARY KEY,
       data JSON
   );
   ```

2. **Insert JSON Data:**
   ```sql
   INSERT INTO customer_data (id, data)
   VALUES (1, '{"name": "John Doe", "age": 30, "address": {"city": "New York", "zip": "10001"}}');
   ```

### **6.3.2 Querying JSON Data**
1. **Query JSON Data:**
   ```sql
   SELECT data.name, data.address.city
   FROM customer_data
   WHERE JSON_EXISTS(data, '$.address.city');
   ```

2. **Update JSON Data:**
   ```sql
   UPDATE customer_data
   SET data = JSON_MERGEPATCH(data, '{"age": 31}')
   WHERE id = 1;
   ```

---

## **6.4 Hands-On: Implementing Blockchain Tables**

### **6.4.1 Creating a Blockchain Table**
1. **Create a Blockchain Table:**
   ```sql
   CREATE BLOCKCHAIN TABLE financial_transactions (
       transaction_id NUMBER PRIMARY KEY,
       transaction_date DATE,
       amount NUMBER
   ) NO DROP UNTIL 365 DAYS IDLE
   NO DELETE LOCKED
   HASHING USING "SHA2_512" VERSION "v1";
   ```

2. **Insert Data:**
   ```sql
   INSERT INTO financial_transactions (transaction_id, transaction_date, amount)
   VALUES (1, SYSDATE, 1000);
   ```

### **6.4.2 Verifying Blockchain Integrity**
1. **Verify Blockchain Integrity:**
   ```sql
   SELECT DBMS_BLOCKCHAIN_TABLE.VERIFY_ROWS('FINANCIAL_TRANSACTIONS') FROM dual;
   ```

2. **Check Blockchain Table Metadata:**
   ```sql
   SELECT table_name, blockchain
   FROM user_tables
   WHERE blockchain = 'YES';
   ```

---

## **6.5 Hands-On: Using JSON Relational Duality**

### **6.5.1 Creating a Duality View**
1. **Create a Relational Table:**
   ```sql
   CREATE TABLE employees (
       emp_id NUMBER PRIMARY KEY,
       emp_name VARCHAR2(100),
       emp_salary NUMBER
   );
   ```

2. **Create a Duality View:**
   ```sql
   CREATE JSON DUALITY VIEW employee_json AS
   SELECT JSON {
       'empId': emp_id,
       'empName': emp_name,
       'empSalary': emp_salary
   }
   FROM employees;
   ```

### **6.5.2 Querying and Updating Data**
1. **Query JSON Data:**
   ```sql
   SELECT * FROM employee_json
   WHERE JSON_EXISTS(data, '$.empName');
   ```

2. **Update JSON Data:**
   ```sql
   UPDATE employee_json
   SET data = JSON_MERGEPATCH(data, '{"empSalary": 5000}')
   WHERE JSON_VALUE(data, '$.empId') = 1;
   ```

---

## **6.6 Summary of Oracle Database 21c and 23c Features**

| **Feature**                     | **Description**                                                                 |
|----------------------------------|---------------------------------------------------------------------------------|
| **Native JSON Datatype**         | Provides native support for storing and querying JSON data.                     |
| **Blockchain Tables**            | Provides tamper-proof data storage for high-integrity applications.             |
| **JSON Relational Duality**      | Combines the benefits of relational and JSON data models.                       |
| **AutoML for In-Database Machine Learning** | Automates the process of building and deploying machine learning models. |
| **SQL Firewall**                 | Protects against SQL injection attacks.                                         |
| **Enhanced Sharding**            | Improves scalability and performance for distributed databases.                 |

---

## **6.7 Key Takeaways**
- Oracle Database 21c and 23c introduced cutting-edge features like **native JSON datatype**, **blockchain tables**, and **JSON Relational Duality**.
- These features cater to modern application development and data management needs.
- Hands-on implementation of these features is essential for DBAs to maximize their benefits in modern environments.

---

