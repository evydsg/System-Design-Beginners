# **MapReduce**

## **Overview**

MapReduce is a programming model designed for processing and generating large datasets efficiently. It is particularly useful for distributed computing across vast amounts of data, such as terabytes or even petabytes. This model enables parallel processing, allowing data to be handled across multiple nodes in a distributed system.

A practical example of MapReduce is processing a dataset with a billion rows of names and Social Security Numbers (SSNs), where we need to redact SSNs while retaining names.

## **Data Processing Methods**

Before diving into MapReduce, it's essential to understand the two primary data processing models:

### **Batch Processing**

- Data is collected over a specific period and processed in large batches.
- Does not operate in real-time; instead, it runs scheduled jobs.
- Example: Counting word frequency in a book or generating daily/weekly reports.

### **Stream Processing**

- Processes data in real-time as it is received.
- Data is handled in its raw, unbatched form.
- Example: Redacting a customer's credit card expiration date or last name immediately upon payment.

## **MapReduce Framework**

A MapReduce system, such as Apache Hadoop, consists of one **master node** and multiple **worker nodes (slave nodes)**.

### **Components and Workflow**

1. **Master Node**
    - Manages job distribution across worker nodes.
    - Monitors task execution and handles failures by reassigning tasks.
2. **Worker Nodes**
    - Perform the actual data processing.
    - Each worker receives a portion of data and executes the MapReduce program.
3. **Map Phase**
    - Each worker processes its assigned data and applies a mapping operation.
    - Example: In a word count scenario, it creates key-value pairs where the key is the word, and the value is its frequency.
4. **Shuffle and Sort Phase**
    - Groups all key-value pairs with the same key across worker nodes.
    - Example: If "The" appears 3 times in worker 1, 7 times in worker 2, and 100 times in worker 3, these values are aggregated.
5. **Reduce Phase**
    - The grouped data is processed to produce final results.
    - Example: Summing up word frequencies and storing the output in a database.

## **History of MapReduce**

MapReduce was introduced by Google engineers to address the challenges of processing massive datasets efficiently while handling failures, such as node partitions. The model ensures reliability and scalability by distributing workloads across multiple machines.