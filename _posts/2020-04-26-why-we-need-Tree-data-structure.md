# Why we need Tree Data Structure?

## 1. Why Choose Trees

### 1.1 Definition

As we known, tree is a kind of data structure, which contains a set of nodes connected by directed or undirected.  It's a *non-linear* data structure in logical, compared to arrays, or string.

### 1.2 Comparison with other data structure

- Basic Data Structure

  There are many basic data structures, such as arrays, linked lists, queues and stacks. They're simple and easy to implement, but not good at performance. For example, if there is a data set with size `n`, we want to access or search an element in this data set, the time cost will be in `O(n)` for queues, stacks and unsorted linked lists.   The insertion and deletion should be run in `O(1)` for queues, stacks and unsorted linked lists.

- Hash table

  How about hash table? Theoretically,  time complexity of insertion, looking-up and deletion is constant time `O(1)`, and the worst case is `O(n)`. For trees, take Binary Search Tree as an example, for average case, it takes `O(logn)` time to insert a new node or look up. `O(logn)` is not as fast as constant time but rather fast.  

  It seems we should prefer hash table over trees, but hash table has some significant drawbacks:

  - Collision, there is huge probability that collision shows up in hash table. Even thoug there are solutions, but at the worst case it costs `O(n)`
  - Space, we need eastimate how many items saved in the array for initialization hash table, and extra space used since the collision.  
  - Unsorted, the elements stored in hash table are unsorted, in some circumstance is very not convenient .

## 2. Binary Trees



## 3. Binary Search Tree





## 4. Review and Comparison

