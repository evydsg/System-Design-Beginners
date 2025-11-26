# Caching

## Overview

Caching is the process of storing copies of data in a location that allows for faster access. It is widely used to reduce latency, improve throughput, and decrease network costs. While caching provides significant performance improvements, its limited capacity requires efficient management strategies.

## CPU Cache

- The CPU cache is the fastest memory, allowing rapid read and write operations compared to RAM and Disk.
- Even though the same data exists in RAM or Disk, storing it in the CPU cache improves processing speeds.
- However, cache memory is limited in size, typically measured in kilobytes or megabytes.

## How Caching Works

1. **Client-side Caching**
    - The browser checks its cache (disk or memory) before making network requests.
    - If data is found in the cache (**cache hit**), it is used directly.
    - If the data is missing or expired (**cache miss**), a network request is made.
2. **Server-side Caching**
    - Data can be cached on the server to reduce database access.
    - Frequently accessed data, such as viral tweets, is stored in cache to enhance response time.

## Cache Performance Metrics

- **Cache Hit Ratio**: Measures the efficiency of caching by calculating:
    
    A higher ratio indicates better caching efficiency.
    

## Caching Strategies

### 1. Write-Around Cache

- New data is written directly to disk, skipping the cache initially.
- Data is only cached if accessed later.
- Efficient for storing large amounts of infrequently accessed data.

### 2. Write-Through Cache

- Data is written to both the cache and disk simultaneously.
- Ensures data consistency between cache and disk.
- Increases memory load as all writes go to the cache.

### 3. Write-Back Cache

- Data is written to cache first and later copied to disk.
- Reduces latency but increases risk of data loss in case of a system crash.
- More efficient for frequent writes.

## Cache Eviction Policies

Since cache storage is limited, an **eviction policy** determines which data to remove when the cache is full.

### 1. FIFO (First-In, First-Out)

- The oldest cached data is removed first.
- Simple to implement but may evict frequently used data prematurely.

### 2. LRU (Least Recently Used)

- Removes data that has not been accessed for the longest time.
- Assumes that older, unused data is less likely to be needed again.
- Commonly used in systems like Twitter to retain frequently accessed content.

### 3. LFU (Least Frequently Used)

- Removes the data accessed the least number of times.
- Uses a frequency count to track data usage.
- May cause issues with older data that was accessed frequently in the past but is no longer relevant.

## Real-Life Example: Web Browser Caching

- Browsers cache static files (e.g., images, JavaScript, CSS) to avoid unnecessary network requests.
- Example: A JavaScript file, `main.cf2a0447c0ac9f9e.js`, is stored in disk cache, significantly reducing load time.
- Disabling the cache increases request time (e.g., 123 ms vs. 11 ms), demonstrating the benefits of caching for improving user experience.