 <b> Oracle Database Versions: A Technical Reference Guide for DBAs.</b> 

This chapter introduces Oracle Database's evolution, its major milestones, and the distinction between Long-Term Support (LTS) and Innovation Releases.

<br>

# **Chapter 1: Introduction to Oracle Database Evolution**

<br>



## **1.1 History of Oracle Database**

Oracle Database, developed by Oracle Corporation, is one of the most widely used relational database management systems (RDBMS). <br>Its history spans over four decades, with each version introducing groundbreaking features that have shaped the database industry.
<br>
### **Key Milestones:**
| **Year**  | **Version**       | **Key Features**                                                                                   |
|-----------|-------------------|---------------------------------------------------------------------------------------------------|
| **1979**  | Oracle V2         | First commercially available SQLbased RDBMS. <br> Introduced the concept of a relational database. |
| **1983**  | Oracle V3         | Written in C, making it portable across platforms. <br> Introduced transactions and commit/rollback functionality. |
| **1984**  | Oracle V4         | Introduced read consistency. <br>  Added support for multiVread consistency (MVCC).    |
| **1985**  | Oracle V5         | Introduced clientserver architecture. <br>  Supported distributed queries.                    |
| **1988**  | Oracle V6         | Introduced PL/SQL (Procedural Language/SQL). <br>  Added rowlevel locking and hot backups.     |
| **1992**  | Oracle 7          | Introduced triggers, stored procedures, and declarative referential integrity. <br>  Added support for distributed databases. |
| **1997**  | Oracle 8          | Introduced objectrelational features. <br>  Added Recovery Manager (RMAN) for backup and recovery. |
| **1999**  | Oracle 8i         | Focused on internet computing. <br>  Introduced Java support and Oracle Internet File System (iFS). |
| **2001**  | Oracle 9i         | Introduced Real Application Clusters (RAC) for high availability. <br>  Added Oracle Streams for data replication. |
| **2003**  | Oracle 10g        | Focused on grid computing. <br>  Introduced Automatic Storage Management (ASM) and Flashback Database. |
| **2007**  | Oracle 11g        | Introduced Real Application Testing (RAT) and Advanced Compression. <br>  Added EditionBased Redefinition (EBR) for online upgrades. |
| **2013**  | Oracle 12c        | Introduced multitenant architecture (Pluggable Databases). <br>  Added InMemory Column Store for faster analytics. |
| **2019**  | Oracle 19c        | LongTerm Support (LTS) release. <br>  Introduced automatic indexing and realtime statistics.  |
| **2023**  | Oracle 23c        | Latest LTS release. <br>  Introduced JSON Relational Duality and SQL Firewall.                  |

<br>

## **1.2 Major Milestones and Innovations**

Oracle Database has consistently introduced innovations that have redefined the database industry. Below are some of the most significant milestones:

### **1.2.1 PL/SQL (Oracle 6)**
- PL/SQL (Procedural Language/SQL) allowed developers to write procedural logic within the database.
- Enabled the creation of stored procedures, functions, and triggers.

### **1.2.2 Real Application Clusters (RAC) (Oracle 9i)**
- RAC allowed multiple instances to access a single database, providing high availability and scalability.
- Enabled applications to scale horizontally across multiple servers.

### **1.2.3 Automatic Storage Management (ASM) (Oracle 10g)**
- ASM simplified database storage management by automating file placement and striping.
- Improved performance and reduced administrative overhead.

### **1.2.4 Multitenant Architecture (Oracle 12c)**
- Introduced Pluggable Databases (PDBs) and Container Databases (CDBs).
- Enabled database consolidation and simplified management.

### **1.2.5 In-Memory Column Store (Oracle 12c)**
- Allowed data to be stored in memory in a columnar format.
- Improved performance for analytical queries.

### **1.2.6 Automatic Indexing (Oracle 19c)**
- Automatically created and dropped indexes based on workload patterns.
- Reduced the need for manual index tuning.

### **1.2.7 JSON Relational Duality (Oracle 23c)**
- Combined the benefits of relational and JSON data models.
- Enabled developers to work with both structured and semi-structured data seamlessly.

<br>

## **1.3 Long-Term Support (LTS) vs. Innovation Releases**

Oracle Database releases are categorized into two types: **Long-Term Support (LTS)** and **Innovation Releases**. Understanding the difference between these is critical for planning upgrades and ensuring stability.

### **1.3.1 Long-Term Support (LTS) Releases**
- **Purpose:** Provide stability and extended support for production environments.
- **Support Duration:** Typically supported for 5-10 years, with extended support options.
- **Examples:** Oracle 19c (supported until 2027), Oracle 23c (supported until 2033).
- **Key Features:** Focus on performance, stability, and security enhancements.

### **1.3.2 Innovation Releases**
- **Purpose:** Introduce new features and technologies for testing and evaluation.
- **Support Duration:** Short-term support (typically 1-2 years).
- **Examples:** Oracle 21c (innovation release for testing new features).
- **Key Features:** Focus on cutting-edge technologies like blockchain, machine learning, and JSON.

### **1.3.3 Choosing Between LTS and Innovation Releases**
- **Production Environments:** Always use LTS releases for stability and long-term support.
- **Testing and Development:** Use Innovation Releases to evaluate new features before they are included in LTS releases.

<br>

## **1.4 Summary of Oracle Database Versions**

| **Version** | **Release Year** | **Key Features**                                                                 |
|-------------|------------------|---------------------------------------------------------------------------------|
| Oracle 7    | 1992             | PL/SQL, triggers, stored procedures, distributed databases.                     |
| Oracle 8i   | 1999             | Internet computing, Java support, partitioning.                                 |
| Oracle 9i   | 2001             | Real Application Clusters (RAC), Oracle Streams, XML DB.                        |
| Oracle 10g  | 2005             | Grid computing, Automatic Storage Management (ASM), Flashback Database.         |
| Oracle 11g  | 2007             | Real Application Testing (RAT), Advanced Compression, Edition-Based Redefinition.|
| Oracle 12c  | 2013             | Multitenant architecture, In-Memory Column Store, Adaptive Query Optimization.   |
| Oracle 18c  | 2018             | Polymorphic Table Functions, Active Data Guard DML Redirection.                 |
| Oracle 19c  | 2019             | Automatic Indexing, Real-Time Statistics, SQL Quarantine.                      |
| Oracle 21c  | 2020             | Native JSON Datatype, Blockchain Tables, AutoML for in-database machine learning.|
| Oracle 23c  | 2023             | JSON Relational Duality, SQL Firewall, Enhanced Sharding.                      |

---

## **1.5 Key Takeaways**
- Oracle Database has evolved significantly over the years, introducing features like PL/SQL, RAC, multitenancy, and in-memory processing.
- Long-Term Support (LTS) releases are ideal for production environments, while Innovation Releases are best for testing new features.
- Understanding the history and evolution of Oracle Database helps DBAs make informed decisions about upgrades and migrations.

<br>
