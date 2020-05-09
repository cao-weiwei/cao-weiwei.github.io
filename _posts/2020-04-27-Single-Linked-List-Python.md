---
layout: default
title: Data Structure - Single Linked List in Python
date: 2020-05-08 23:00:00 -0400
published: 2020-05-08 23:00:00 -0400
comments: true
tags: [linked list, data structure, algorithm, Python]
github: "https://github.com/cao-weiwei/"
noimage: true
---
In this post, let's go through linked list in a brif way. I'll introduce basic operations of linked list in Python.🤓

<!--more-->

## Single Linked List

### 1. Strcuture
Below is a simple depiction of a single linked list:
<img src="/assets/images/posts/Single-Linked-List-Python/01_linked_list.png" style="zoom:70%;" />


Every linked list consists of nodes, we call the first node as 'head' and the last as 'tail', and for each node it has two components:
- data, it allows a node in the linked list to **store an element** of data that can be of type string, character, number, or any other type of object.
- next, it is **a pointer** that points from one node to another.

Sometimes, we may need a dummy head in the linked list that can help us with intrusion or deletion the first node.

### 2. Difference with Array

#### Insertion/ Deletion

- If we are given the exact pointer after which we have to insert another node or delete a node, it will be a constant-time operation.
- However, the insertion/deletion operation is in `O(n)` operations for insertion/deletion of value at the array. Due to the shifting of the elements, the time complexity is `O(n)`.

#### Accessing Elements

- Accessing an n-th element in a linked list is an `O(n)` operation given that you have access to the head node of the linked list. 
- It is a constant time operation to access elements in arrays, if given an array and an index.

### 3. Implementation

#### 1). General classes
Single linked lists contain two kinds of classes:
- `Node` class, Every node is going to consist of `data` and `next`. 
- `LinkedList` class, except constructor, it initially contains `print_list()` methos to show each node's data.


```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
    
    def print_list(self):
        """
        it will print out the data of each node from head to tail.
        """
        cur_node = self.head
        while cur_node:
            print(cur_node.data)
            cur_node = cur_node.next
         
```

#### 2). Insertion

Now we'll insert elements in a linked list by different ways:
- `append`, the append method will insert an element at the end of the linked list. 

  For append method, we should consider two kinds of situations:

  - if the linked list is empty, or
  - if the linked list is not empty.

  ```python
  def append(self, data):
    """
    the append method will insert an element at the end of the linked list. 
    """
    new_node = Node(data)	# create a node that will be inserted
  
    if not self.head:  # the linked list is empty
      self.head = new_node
      return
  
    last_node = self.head  # the linked list is not empty
    while last_node.next:
      last_node = last_node.next
      last_node.next = new_node
  ```

  

- `prepend`, the prepend method will insert an element at the beginning of the linked list.

  ```python
  def prepend(self, data):
    """
    it will insert an element at the beginning of the linked list.
    """
    new_node = Node(data)
    new_node.next = self.head
    self.head = new_node
  ```

  

- `insert_after_node`, this method will insert an element after a given node.

  If we want to insert an element at somewhere(except head and tail) of the linked list, then this method will work. First, let's break down the steps of solving this kind of problem:

  - First of all, we will create a new node based on the given data;
  - Next, we need to check if the node to be inserted after is in the linked list or not(here just check whether it is a non-node);
  - Last, we change the next pointer of the previous node to point to the new node.

  ```python
  def insert_after_node(self, pre_node, data):
    """
    it will insert an element after a given node.
    """
    if not pre_node:
      print("Previous node is None")
      return
  
    new_node = Node(data)
    new_node.next = pre_node.next
    pre_node.next = new_node
  ```

  


#### 3). Deletion

##### 3-1). Deletion by Value

To delete a node in the linked list, first is to find the node to be deleted by traversing the linked list first. Then, delete that node and update the rest of pointers. However, to solve this problem, we need to handle two cases:

- Node to be deleted is head, or 
- Node to be deleted is not head.


```python
def delete_node(self, data):
  """
  this method will delete the given data node if existed in the linked list
  """
  cur_node = self.head
  if cur_node and cur_node.data == data:  # deal with the case of head
    self.head = cur_node.next
    cur_node = None
    return
  else:
    pre_node = None    # other cases
    while cur_node and cur_node.data != data:
      pre_node = cur_node
      cur_node = cur_node.next
            
    if not cur_node: return
    pre_node.next = cur_node.next
    cur_node = None
```




##### 3-2). Deletion by position

Now, let's delete a node based on position rather than value. Again, we’ll consider the above twos cases

```python
def delete_node_at_pos(self, pos):
  """
  it will delete a node based on given position. 
  """
  cur_node = self.head
  if cur_node and pos == 0: # deal with the case of head
    self.head = cur_node.next
    cur_node = None

  count = 0 # other cases
  pre_node = None
  while cur_node and count != pos:
    pre_node = cur_node
    cur_node = cur_node.next
    count += 1
  
  if not cur_node: return
  pre_node.next = cur_node.next
  cur_node = None
```




#### 4). Length

There are two ways to calculate the number of nodes in a linked list, which are iterative and recursive manners.

##### 4-1). Iterative solution

```python
def len_iterative(self):
  """
  return the number of nodes in a linked list, using iterative method
  """
  count = 0;
  cur_node = self.head
  while cur_node:
    count += 1
    cur_node = cur_node.next
  
  return count
        
```

##### 4-2). Recursive solution

Before we start the recursive solution, let's look the following diagram that could help us understand the method more specific.

<img src="/assets/images/posts/Single-Linked-List-Python/02_recursion_in_linkedlist.png" style="zoom:60%;" />

For any recursive method, we need a base case. In this class, the base case is whether or not we've encountered the end of the linked list which means the `None` pointer.

- if we reach the end of the linked list, it should return `0`, otherwise;
- call the recursive method and pass in the next node and plus `1`. 

```python
def len_recursive(self, node):
  """
  return the number of nodes in a linked list, using recursive method
  """
  if not node: return 0 # base case
  return 1 + self.len_recursive(node.next)
```




#### 5). Node Swap

Now, assume we have two keys corresponding to the data element in the nodes, we would like to swap the two nodes in a linked list, what should we do?

One way to solve this is by iterating the linked list and keeping track of certain pieces of information that are going to be helpful.

- We can start from the first node of the linked list and keep track of both the previous and the current node.
- If the data element of the node that we’re on matches one of the two keys, we record the information and repeat the process for the second node

There are two cases that we’ll have to cater for:
- Node 1 and Node 2 are not head nodes.
- Either Node 1 or Node 2 is a head node.


```python
def swap_nodes(self, data_1, data_2):
    """
    it will swap two nodes if they're existed in the linked list
    """
    if data_1 == data_2: return    # two data are duplicate.
    
    pre_1, cur_1 = None, self.head  # looking for the data_1 and its previus node
    while cur_1 and cur_1.data != data_1:
        pre_1 = cur_1
        cur_1 = cur_1.next
        
    pre_2, cur_2 = None, self.head  # looking for the data_2 and its previuos node
    while cur_2 and cur_2.data != data_2:
        pre_2 = cur_2
        cur_2 = cur_2.next
        
    if not cur_1 or not cur_2: return  #cur_1 or cur_2 is none, means one of the data is no existed in linked list
    
    if pre_1:
        pre_1.next = cur_2
    else:    # data_1 is the head node
        self.head = cur_2
    if pre_2:
        pre_2.next = cur1
    else:    # data_2 is the head node
        self.head = cur_1
        
    cur_2.next, cur_1.next = cur_1.next, cur_2.next    # swap the two nodes.
    
```




#### 6). Reverse 

In this part, let's talk about how to reverse a singly linked list in an iterative way and a recursive way. Before getting started, let's know how to reverse a linked list first.

<img src="/assets/images/posts/Single-Linked-List-Python/03_reverse_linked_list.png" style="zoom:70%;" />

##### 6-1). Iterative implementation
The key idea is that we’re reversing the orientation of the arrows. For example, node A is initially pointing to node B but after we flip them, node B points to node A. The same is the case for other nodes. 


```python
def reverse_itr(self):
  """
  reverse the linked list, using iterative method
  """
  pre, cur = None, self.head
  while cur:	# three pointers for reversing
    nxt = cur.next;
    cur.next = prev
    prev = cur
    cur = nxt
  # new head after reversing
  self.head = prev    
```




##### 6-2). Recursive Implementation

The crux of recursive solution is as follows:
- the base case;
- assume we solve the simplest problem, which in this case is to reverse just ONE pair of nodes
- the rest nodes of the linked list will repeat above process.

```python
def reverse_rec(self):
  """
  it will reverse the linked list, using recursive method
  """
  def _reverse(pre, cur):
    if cur:
      _reverse(cur, cur.next)
      cur.next = pre
    else:
      self.head = pre

  _reverse_recursive(pre=None, cur=self.head)    # setting the head, which is the pre
```




#### 7). Remove Duplicates

We can use a hash-table or dictionary in Python to remove duplicates from a linked list.

- The general idea is to go through the linked list once and keep track of all the data held at each of the nodes.  
- Use a dictionary to keep track of the data elements that we encounter to determine whether in the dictionary.


```python
def remove_deuplicates(self):
  """
  it will remove duplicate data held by nodes, using a dictionary.
  """
  dup_data = dict()
  cur = self.head
  pre = None
  
  while cur:
    if cur.data in dup_data: # if the data has existed in the dictionary, then removing it
      pre.next = cur.next
      cur = None
    else:
      dup_data[cur.data] = 1 # else, put the data in the dictionary
      pre = cur
    
    cur = pre.next
```




#### 8). Nth-from-last Nodes

Now let's dive into the solutions:
1. ragualer way, counting the length, break down this solution in two simple steps:
    - Calculate the length of the linked list.
    - Count down from the total length until n is reached.

Let's look into the implementation:


```python
def print_nth_from_last(self, n):
    """
    to find the data of n-th node from the last, using length of the linked list
    """
    total_len = self.len_iterative()
    
    cur = self.head 
    while cur:    # countdown using total_len decrement
        if total_len == n:
            return cur.data
        total -= 1
        cur = cur.next
    if not cur:
        print(str(n) + "is greater than the length of the linked list.")
        return
```

2. two pinters pattern, when fast pointer or next node of fast pointer is None, the slow pointer will reach the n
    - `p` will point to the head node.
    - `q` will point n nodes beyond head node.
    

About two pointers pattern, the slow pointer will at the middle of the linked list, if the fast node is none or fast node's next node is none. This because, in even length fast node will be the `(length // 2 + 1)`, in odd length the fast node will be the excat middle one.

Here, this pattern can be used to look for the nth-node from the last node. The idea behind this solution is that the gap between p and q is the n, when p or q.next is None


```python
def print_nth_from_last(self, n):
    """
    to find out the data of n-th node from the last, using two pointer pattern
    """
    p = q = self.head
    
    count = 0
    while q:    # q points to the n-th node from the head
        count += 1    # count += 1, because q have pointed 1 node already.
        if count >= n: break
        q = q.next
    
    if not q: print(str(n) + "is greater than the length of the linked list.")
    
    while p and q.next:  #gap between p and q is n, when p or q.next is None, the n-th node from last is found
        p = p.next
        q = q.next
        
    return p.data
```

Both the solutions have been made part of the `LinkedList` class. We can call the solution of the choice by passing in `1` or `2` as `method` to `print_nth_from_last(self, n, method)`.

