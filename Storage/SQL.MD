# **SQL and B+ Trees**

### **SQL Databases (RDBMS)**

- SQL databases, also known as **Relational Database Management Systems (RDBMS)**, store persistent data using tables.
- They structure data efficiently within disk storage, allowing for optimized reading and writing operations.
- Data is formatted into well-defined fields, making it easily **queryable**.

### **B+ Trees and Query Efficiency**

- SQL databases achieve **efficient queries** using a data structure called a **B+ Tree**.
- **B+ Trees** are multi-way trees, meaning each node can have more than two children.
- **Leaf nodes** store all data and are linked in **sorted order**, optimizing retrieval.
- Unlike **B-Trees**, where interior nodes store data, **B+ Trees store data only in leaf nodes**.

### **B+ Tree Structure**

- Each node can have a maximum of **M children** and contains **M-1 keys**.
- Example: A root node with keys **[2, 5]** would have three children:
    - **First child:** `[0, 1]` (values < 2)
    - **Second child:** `[3, 4]` (values between 2 and 5)
    - **Third child:** `[6, 7]` (values > 5)
- The **keys act as separators** that divide subtrees, improving search efficiency.

### **Indexing in B+ Trees**

- **Indexing** is a technique that speeds up data retrieval operations on a database table.
- It comes at the **cost of additional writes and storage space** to maintain the index structure.
- Example: A database with **names mapped to phone numbers** can use the **name** field as an index to enable **faster lookups**.
- While indexing enhances performance, it has **downsides**, which are beyond the scope of this discussion.

## **How Data is Stored in an SQL Database**

### **Tables and Primary Keys**

- Data in an SQL database is stored inside **tables**.
- A **table** organizes data into **rows**, where each row represents a **single record**.
- Each record is uniquely identified by a **Primary Key**.
- A **Primary Key** ensures that no two records in the table have the same identifier.

### **Example: Storing Phone Numbers and Names**

Suppose we want to store **people's names and their phone numbers** in a table called `People`, where the **PhoneNumber** acts as the primary key.

Before inserting any records, we must define the table structure using SQL:

```sql
CREATE TABLE People (
    PhoneNumber INT PRIMARY KEY,
    Name VARCHAR(100)
);

```

- **VARCHAR** (pronounced "var-car") is a **variable-length string data type** that can store numbers, letters, and special characters.
- The **PhoneNumber** field is designated as the **Primary Key**, ensuring each entry is unique.

### **Using Foreign Keys for Relationships**

Now, suppose we want to associate each phone number with an **address** in a separate table called `Homes`.

- We need to **ensure that no PhoneNumber is inserted into `Homes` unless it already exists in `People`**.
- This is enforced using a **Foreign Key constraint**, which links `Homes` to `People` via the `PhoneNumber` field.

```sql
CREATE TABLE Homes (
    PhoneNumber INT,
    Address VARCHAR(255),
    FOREIGN KEY (PhoneNumber) REFERENCES People(PhoneNumber)
);

```

- The **FOREIGN KEY** enforces a relationship between the `Homes` and `People` tables.
- Every **PhoneNumber in `Homes` must exist in `People`**, ensuring data consistency.

## **Joins in SQL**

### **What are Joins?**

- **Joins** allow us to **combine records** from two or more tables based on a **common column**.
- In our example, we want to retrieve the **names and addresses** of people using their `PhoneNumber`.

### **Example: Using an SQL JOIN**

To fetch names and addresses from the `People` and `Homes` tables, we use an **INNER JOIN** on the `PhoneNumber` column:

```sql
SELECT People.Name, Homes.Address
FROM People
JOIN Homes ON People.PhoneNumber = Homes.PhoneNumber;

```

- The **JOIN** statement ensures that only records with matching `PhoneNumber` values in both tables are returned.
- This means a person must have an entry in **both tables** to appear in the results.

---

## **Trade-offs of Relational Database Management Systems (RDBMS)**

RDBMSs follow the **ACID** properties to ensure **reliability, consistency, and data integrity** in database transactions.

### **ACID Properties**

ACID stands for:

1. **Atomicity** – Ensures all operations in a transaction are completed or none at all.
2. **Consistency** – Guarantees that a transaction brings the database from one valid state to another.
3. **Isolation** – Ensures concurrent transactions do not interfere with each other.
4. **Durability** – Ensures that committed transactions are permanently saved, even in case of a system failure.

---

### **Durability**

- Once a transaction **completes successfully**, its changes are **permanent** and will not be lost due to system failures.
- **Example:**
    - If an application transfers funds from one account to another, and the system crashes **after** the transaction, the transaction **remains recorded** in the database.

---

### **Atomicity**

- A transaction is **all-or-nothing**—**either all operations succeed, or none are executed**.
- If **one step fails**, the **entire transaction is rolled back**, ensuring no partial updates occur.
- **Example:**
    - Alice has **$1000**, and Bob has **$500** in their bank accounts.
    - Alice transfers **$500** to Bob.
    - If the database crashes **midway**, Atomicity ensures that:
        - Alice's **$500 is NOT deducted** if Bob’s balance update fails.
        - The transaction **only commits if both operations succeed**.
    - Without Atomicity, the money might be **lost** if only one step was completed.

## **ACID Properties in Relational Databases**

### **Isolation**

- **Isolation** ensures that transactions are executed independently, preventing interference from concurrent transactions.
- While a transaction is **in progress**, its intermediate states remain **invisible** to other transactions.
- As a result, transactions appear **serialized**, meaning they execute **sequentially** rather than concurrently.

### **Example: Isolation in Transactions**

Consider Alice and Bob’s bank accounts:

- **Alice has $1000**, and Bob has **$500**.
- A **first transaction** attempts to:
    1. Deduct **$500** from Alice’s account.
    2. Add **$500** to Bob’s account.
    3. **Commit the transaction**.

Before this transaction **commits**, a **second transaction** occurs:

- The second transaction **adds $200** to Alice’s account and commits.
- Since the first transaction was **not yet committed**, the second transaction **reads an uncommitted value**—causing a **dirty read**.

### **Dirty Read Issue**

- A **dirty read** occurs when a transaction reads data that has been modified by another transaction **before it has been committed**.
- To **maintain isolation**, the **second transaction should wait** for the first one to commit before proceeding.

### **Serialization**

- Transactions should be executed **sequentially** as if they are **running in isolation**.
- Serialization ensures that:
    - The **order of execution** is maintained.
    - The **effects of a transaction** become visible **only after it has been committed**.
    - **Dirty reads are prevented**.

---

### **Consistency**

- **Consistency** ensures **data integrity** by enforcing **predefined rules and constraints**.
- Every transaction must transition the database **from one valid state to another**.

### **Example: Consistency Constraints**

- A bank database **defines a rule** that an **account balance cannot be negative**.
- If a transaction attempts to **withdraw more than the available balance**, the database **rejects** the transaction to maintain **consistency**.

Consistency guarantees that all transactions:

- Follow the database’s **rules and constraints**.
- Preserve **data validity** across multiple transactions.