# Data Structures
## Fundamental Abstract Data Types
- container
- dictionary
- priority queue

## Contiguous vs Linked Structures
Contiguous structures use single slabs of memory. These include arrays, heaps, matrices, and hash tables.

Linked structures use chunks of memory tied together by pointers. Includes lists, trees, graph adjacency lists.

An array is a contiguously-allocated structure. They consist of fixed-size records that can be accessed by an index. Access is constant-time.

In a linked list, each element contains a pointer to the next. Pointers represent a memory address. 

The list is the simplest linked structure. It supports search, insert, and delete operations.

A doubly-linked list has a pointer to the previous element as well as the next.

A _container_ is a way to describe a structure that permits storage and retrieval of items independent of content. See _Stacks and Queues_.

## Stacks and Queues
Stacks provide LIFO retrieval. Supported operations are _push_ and _pop_.

Queues provide FIFO retrieval. Supported ops are _put_ and _get_.

## Dictionaries
Dictionaries provide access via _key_ (or _hash_). The underlying implementation of a dictionary might use an array, linked list, or stack, depending on its purpose.

The primary operations supported are insert, delete, and search.'

A _hash table_ is a practical way to maintain a dictionary.

## Binary Search Trees
A binary search tree is based on a sorted doubly-linked. Each element points to an "above" and "below" node.

In an unsorted list, insertion and deletion can be done in _O(1)_ time but worst-case searching is _O(n)_. A dictionary implemented with a binary search tree supports all operations _O(h)_ time, where _h_ is the height of the tree.

A perfectly balanced tree (_h_ is the smallest height) can be searched in logarithmic time.

## Priority Queues
Similar to a dictionary and queue, but the key (or some component of it) is relevant to ordering. Operations enable find and delete by minimum or maximum key. 

## Other Data Structures

- Strings
- Tuples
- Graphs
- Sets