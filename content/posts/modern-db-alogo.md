---
title: Modern database algorithms
date: 2023-12-11
linktitle: DB Algos
menu:
  main:
    name: DB Algos
    weight: 11
categories:
  - "System design"
  - "Algorithims"
tags:
  - "System design"
  - "Algorithims"
  - "Database"    
---

## Skip list `probabilistic data structure`
A **skip list** is a data structure that allows for efficient searching, insertion, and deletion of elements in a sorted collection, such as a linked list. It was designed to provide logarithmic-time average-case complexity for these operations, making it an alternative to more traditional structures like binary search trees.

### Key Characteristics of Skip Lists:

1. **Levels and Layers:**
   - Skip lists have multiple layers, where each layer represents a different "level" of the data structure.
   - The bottom layer contains all elements in sorted order.
   - Higher layers skip over elements in the lower layers, reducing the number of nodes to traverse during searches.

2. **Nodes:**
   - Each element in the skip list is represented by a node containing a key and, optionally, additional levels of pointers.

3. **Randomization:**
   - Skip lists often use a randomization process to determine the number of levels a node will have. This randomization helps balance the structure and maintain its efficiency.

### Basic Operations:

1. **Search:**
   - Searching in a skip list involves starting from the top-left and moving right and down, stopping when the desired element is found or when there's nowhere further to go.

2. **Insertion:**
   - To insert an element, search for its position in the list, and then, with a certain probability, create additional levels for the new element, linking it appropriately.

3. **Deletion:**
   - Similar to insertion, deletion involves searching for the element and updating the pointers to bypass the node to be deleted.

### Example of a Skip List:

Consider a skip list with elements {1, 2, 3, 6, 7, 9, 12, 15}. The structure might look like this:

```
Level 3:         3 --------------> 7 --------------> 12 --------------> 15
Level 2:         3 --------------> 7 --------------> 12 --------------> 15
Level 1:         1 -------> 3 -------> 6 -------> 7 -------> 9 -------> 12 -------> 15
```

In this example:
- Each node has multiple levels, and higher-level nodes skip over lower-level nodes.
- The search for an element, say 6, would start from the top-left and move down and to the right, stopping when 6 is found.
- Inserting a new element involves determining its level (randomly) and updating pointers accordingly.
- Deleting an element would require adjusting pointers to bypass the node to be deleted.

### Advantages and Disadvantages:

**Advantages:**
- **Efficiency:** Skip lists provide logarithmic average-case time complexity for search, insertion, and deletion operations.
- **Simplicity:** The structure is relatively simple compared to other balanced search structures.

**Disadvantages:**
- **Space Overhead:** Skip lists may consume more memory due to the multiple levels of pointers.
- **Deterministic Version:** The efficiency of skip lists relies on randomization. A deterministic version can be implemented but may require additional considerations for balancing.

Skip lists are used in various applications where efficient searching and dynamic updating of a sorted collection are essential, and their simplicity and performance characteristics make them an attractive choice in certain scenarios.


**List of applications and frameworks that use skip lists:**
1. Redis, uses skip lists in its implementation of ordered sets.
2. RocksDB uses skip lists for its default Memtable implementation.
3. MemSQL uses lock-free skip lists as its prime indexing structure for its database technology.
4. MuQSS, for the Linux kernel, is a cpu scheduler built on skip lists.
5. Apache Portable Runtime implements skip lists
6. Discord uses skip lists to handle storing and updating the list of members in a server
7. Cyrus IMAP server offers a "skiplist" backend DB implementation
8. Lucene uses skip lists to search delta-encoded posting lists in logarithmic time.[citation needed]
9.  The "QMap" key/value dictionary (up to Qt 4) template class of Qt is implemented with skip lists.

Skip lists are also used in distributed applications (where the nodes represent physical computers, and pointers represent network connections) and for implementing highly scalable concurrent priority queues with less lock contention, or even without locking, as well as lock-free concurrent dictionaries. There are also several US patents for using skip lists to implement (lockless) priority queues and concurrent dictionaries