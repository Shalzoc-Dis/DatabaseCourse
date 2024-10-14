Differences between RAM and disk

| RAM           | Disk          |
| :--           | :--           |
| Volatile      | Persistent    |
| Expensive     | Cheap         |
| Limited Space | Lots of Space |
| Fast (nS)     | Slow (ms)     |

Because of the benefits, disk is the place data is usually stored.
A disk drive contains a disk which has **tracks**, in a concentric circle pattern, and **sectors**, wedges just like a circle sectors.
A **file block** is at each intersection between a track and a sector. File blocks are typically 4kiB in size. When we write data, we have to write it in file blocks.
Whenever we want to access or manipulate data, the whole file block has to be loaded into RAM.

We have several different schemes for finding data.
##Pure Disk
Let's say we have 400 bytes in each document/row and say each file block is 4kB. This means we can store 10 rows per block. It we want to store 1 million rows, 
we would need 10^5 blocks. If each read takes a conservative 1ms, we would have searched through the whole volume in 100s. So, the worst case scenario for 
finding an element is 100s.

##Indexing
Let's make a table of all our entries. The table tells us what block a specific entry is in. If each entry takes 10 bytes, we can store 400 of them in one block. 
Since we need to store 10^5 entries, we would need 250 file additional file blocks for the table. Again, each read takes 1ms. Now when we search for some 
information, we can look it up in the table, which takes at most 250ms to scan. Our total time is now at 251ms, adding a millisecond for actually retrieving the data.

##Multi-Level Indexing
Our **index table** from above takes up 250 file blocks of space. What if we have a table to find things in the table? This second table only needs 2500 bytes 
(each row is 10 bytes again) which fits inside one file bloc. Now, we need 3ms to read the data, one for the first table, one for the relevant 
portion of the second table, and one for the file block containing the actual data.

##B-Trees (Balanced Trees)
A B-tree is just a layer of index tables like this. Each one of the tables have several keys and several child pointers associated with them that point
to other notes. A **node** is a pairing of a key and a child pointer.

#Comparing Search Data Structures

###Balanced BST (Binary search)
This is a fast way to search through a database with worst-case of O(log n), making for about 20 search operations with 10^6 entries. Insert and delete operations 
are the same. (In computer science log is assumed to have base 2)

###Unbalanced BST
Since the tree is not balanced, it could be arranged linearly in the worst case, making us do all 10^6 operations. The maximum number of insert and delete operations 
we would have to perform is also 10^6.

###Sorted Array
Finding items would be fast, roughly 20 search operations because we would use binary search. Insert and delete are worse though; because we need to store the data 
contiguously, we would have to shift all 10^6 blocks if we insert before the first one or delete the first one. 

###B-Tree
A B-tree is a specific form of an M-way tree, where m is the maximum number of child pointers each key has. A B-tree of order m has a maximum of m children. Its 
complexity is O(log_m n). If we had 100 child nodes, we would need three I/O operations. Search, insert, and delete are the same in this case.

##Recap

|                | Search | Insert | Delete |
| :------------- | :----- | :----- | :----- |
| Balanced BST   | 20     | 20     | 20     |
| Unbalanced BST | 10^6   | 10^6   | 10^6   |
| Sorted Array   | 20     | 10^6   | 10^6   |
| B-tree         | 3      | 3      | 3      |

# Structure
In BST, each node has a kay and two child pointers. If the key is 20, for instance, the left child pointer could be pointing to all nodes less than 20. The other 
could point to all more than 20.
An M-tree can have several keys per node. This means we have to do more comparisons. For example, a node could have 10, 20, 30 as keys. 10 might point to keys from 
1 to 10. Now, we not only have to compare if our input is greater or less than one key value, we have to do more comparisons.
The reason this can be more efficient is because our primary cost is reading data into RAM. Comparisons are fast by comparison. So, if we can be more accurate and 
avoid reading more unnecessary data by doing a few more comparisons, this is often worth it.
Furthermore, we have to retrieve disk data one file block at a time. We might as well store as many keys in a node as possible because we get the whole file block 
anyway.

#B-Tree Characteristics
A B-tree of order m can have at most m children and m-1 keys. Each key separates two sub-trees, so each child pointer is "in between" each key.
The minimum number of keys any node other than the root can have is ceil(m/2). The root has a minimum of 1 key.
It is important that all the leaves are at the same level. If this is true and the root node has m keys, each layer can have an additional factor of m keys. 
Therefore, if the leaf layer has x keys, the one before will have x/m keys, the one before will have x/m^2 keys, etc.
If the total number of keys we have to accommodate is n, the height of the tree is given by log_n m.

A B-tree grows towards the root. If a key is added and a node can't accept it, a new node is created next to it and one is created above them. This makes it very easy 
to grow and shrink the number of entries. This essentially ensures that we have the fewest index tables as possible.

#Differences Between B-Trees and B+ Trees
A B+ tree has some redundant data. Namely, all keys can be found in the leaf nodes and all leaf nodes are connected together in a linked list. This is important 
should there be lots of range based queries. Instead of searching through the branches of a B-tree, we can just jump from leaf to leaf, saving time.