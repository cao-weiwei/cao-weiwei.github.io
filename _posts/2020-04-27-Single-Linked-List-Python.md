---
layout: default
title: "Single Linked List in Python"
comments: true
categories: data structure and algorithms
tags: [linked list, data structure, algorithm]
github: "https://github.com/cao-weiwei/"
noimage: true
---
## 0Single Linked List

### 1. Strcuture
Below is a simple depiction of a single linked list:
<img src="/Users/caoweiwei/Library/Application Support/typora-user-images/image-20191218165948878.png" alt="image-20191218165948878" style="zoom:33%;" />


Every linked list consists of nodes, and each node has two components:
- data
    - The data component allows a node in the linked list to **store an element** of data that can be of type string, character, number, or any other type of object.
- next
    - The next component in every node is **a pointer** that points from one node to another.
- head
    - The start of the linked list is referred to as the head


### 2. Operations

#### 1). Insertion/ Deletion

- If we are given the exact pointer after which we have to insert another node or delete a node, it will be a constant-time operation.
- However, the insertion/deletion operation is in `O(n)` operations for insertion/deletion of value at the array. Due to the shifting of the elements, the time complexity is `O(n)`.

#### 2). Accessing Elements

- Accessing an n-th element in a linked list is an `O(n)` operation given that you have access to the head node of the linked list. 
- It is a constant time operation to access elements in arrays, if given an array and an index.

#### 3). Contiguous Memory

- Array are contiguous in memory which allows the access time to be constant, whereas, in linked lists, you do not have the luxury of contiguous memory.

### 3. Implementation

#### 1). General classes
Single linked lists contain two kinds of classes:
- `Node` class, Every node is going to consist of `data` and `next`. 
- `LinkedList` class


```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
```

#### 2). Insertion

Now we'll insert elements in a linked list by different ways:
- `append`, the append method will insert an element at the end of the linked list. 
- `prepend`, the prepend method will insert an element at the beginning of the linked list.
- `insert_after_node`, this method will insert an element after a given node.

##### 2-1). Append

For append method, we should consider two kinds of situations:
- if the linked list is empty, or
- if the linked list is not empty.


```python
class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, data):
        """
        the append method will insert an element at the end of the linked list. 
        """
        new_node = Node(data)
        
        if not self.head:  # the linked list is empty
            self.head = new_node
            return
        
        last_node = self.head  # the linked list is not empty
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
```

Now we want some way to verify our append method. For this purpose, let’s create a method called `print_list()`.


```python
class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, data):
        """
        the append method will insert an element at the end of the linked list. 
        """
        new_node = Node(data)
        
        if not self.head:  # the linked list is empty
            self.head = new_node
            return
        
        last_node = self.head  # the linked list is not empty
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
    
    def print_list(self):
        """
        this method will print out the data component of the node from the head node to the last node.
        """
        cur_node = self.head
        while cur_node:
            print(cur_node.data)
            cur_node = cur_node.next
        
```


```python
llist = LinkedList()
llist.append("A")
llist.append("B")
llist.append("C")
llist.append("D")
llist.print_list()
```

    A
    B
    C
    D


##### 2-2). Prepend

Actually, the node calls prepend method will become the head in the linked list.


```python
class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, data):
        """
        the append method will insert an element at the end of the linked list. 
        """
        new_node = Node(data)
        
        if not self.head:  # the linked list is empty
            self.head = new_node
            return
        
        last_node = self.head  # the linked list is not empty
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
        
    def prepend(self, data):
        """
        the prepend method will insert an element at the beginning of the linked list.
        """
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
    
    def print_list(self):
        """
        this method will print out the data component of the node from the head node to the last node.
        """
        cur_node = self.head
        while cur_node:
            print(cur_node.data)
            cur_node = cur_node.next
```


```python
llist = LinkedList()
llist.append("A")
llist.append("B")
llist.append("C")
llist.append("D")
llist.prepend("E")
llist.print_list()
```

    E
    A
    B
    C
    D


##### 2-3). Insert after node

If we want to insert an element at somewhere(except beginning and end) of the linked list, than this method will work. Before we get started coding, let's break down the steps of solving this kind of problem:
- First of all, we will create a new node based on the given data;
- Next, we need to check if the node to be inserted after is in the linked list or not(here just check whether it is a non-node);
- Last, we change the next pointer of the previous node to point to the new node.


```python
class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, data):
        """
        the append method will insert an element at the end of the linked list. 
        """
        new_node = Node(data)
        
        if not self.head:  # the linked list is empty
            self.head = new_node
            return
        
        last_node = self.head  # the linked list is not empty
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
        
    def prepend(self, data):
        """
        the prepend method will insert an element at the beginning of the linked list.
        """
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        
    def insert_after_node(self, pre_node, data):
        """
        this method will insert an element after a given node.
        """
        if not pre_node:
            print("Previous node is None")
            return
        
        new_node = Node(data)
        new_node.next = pre_node.next
        pre_node.next = new_node

    
    def print_list(self):
        """
        this method will print out the data component of the node from the head node to the last node.
        """
        cur_node = self.head
        while cur_node:
            print(cur_node.data)
            cur_node = cur_node.next
        
```


```python
llist = LinkedList()
llist.append("A")
llist.insert_after_node(llist.head.next, "D")
llist.print_list()  
```

    Previous node is None
    A


#### 3). Deletion

##### 3-1). Deletion by Value

In this lesson, we will investigate singly-linked lists by focusing on how one might delete a node in the linked list. 
- In summary, to delete a node, we’ll find the node to be deleted by traversing the linked list first. 
- Then, we’ll delete that node and update the rest of pointers.

To solve this problem, we need to handle two cases:
- Node to be deleted is head, or 
- Node to be deleted is not head.


```python
class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, data):
        """
        the append method will insert an element at the end of the linked list. 
        """
        new_node = Node(data)
        
        if not self.head:  # the linked list is empty
            self.head = new_node
            return
        
        last_node = self.head  # the linked list is not empty
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
        
    def prepend(self, data):
        """
        the prepend method will insert an element at the beginning of the linked list.
        """
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        
    def insert_after_node(self, pre_node, data):
        """
        this method will insert an element after a given node.
        """
        if not pre_node:
            print("Previous node is None")
            return
        
        new_node = Node(data)
        new_node.next = pre_node.next
        pre_node.next = new_node
        
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
    
    def print_list(self):
        """
        this method will print out the data component of the node from the head node to the last node.
        """
        cur_node = self.head
        while cur_node:
            print(cur_node.data)
            cur_node = cur_node.next
        
```


```python
llist = LinkedList()
llist.append("A")
llist.append("B")
llist.append("C")
llist.append("D")

llist.delete_node("B")
if not (llist.delete_node("E")):
    print("E not found in the linked list")

llist.print_list()
```

    E not found in the linked list
    A
    C
    D


##### 3-2). Deletion by position

we will delete a node based on position rather than value. Again, we’ll consider two cases while writing our code:
- Node to be deleted is at position 0, or
- Node to be deleted is not at position 0.


```python
class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, data):
        """
        the append method will insert an element at the end of the linked list. 
        """
        new_node = Node(data)
        
        if not self.head:  # the linked list is empty
            self.head = new_node
            return
        
        last_node = self.head  # the linked list is not empty
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
        
    def prepend(self, data):
        """
        the prepend method will insert an element at the beginning of the linked list.
        """
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        
    def insert_after_node(self, pre_node, data):
        """
        this method will insert an element after a given node.
        """
        if not pre_node:
            print("Previous node is None")
            return
        
        new_node = Node(data)
        new_node.next = pre_node.next
        pre_node.next = new_node
        
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
            
    def delete_node_at_pos(self, pos):
        """
        it will delete a node based on given position. 
        """
        cur_node = self.head
        if cur_node and pos == 0:
            self.head = cur_node.next
            cur_node = None
        
        count = 0
        pre_node = None
        while cur_node and count != pos:
            pre_node = cur_node
            cur_node = cur_node.next
            count += 1
        if not cur_node: return
        pre_node.next = cur_node.next
        cur_node = None
    
    def print_list(self):
        """
        this method will print out the data component of the node from the head node to the last node.
        """
        cur_node = self.head
        while cur_node:
            print(cur_node.data)
            cur_node = cur_node.next
        
```


```python
llist = LinkedList()
llist.append("A")
llist.append("B")
llist.append("C")
llist.append("D")

llist.delete_node_at_pos(0)

llist.print_list()
```

    B
    C
    D


#### 4). Length

Now, we’ll calculate the length or the number of nodes in a given linked list. We’ll be doing this n both an `iterative` and `recursive` manner.

##### 4-1). Iterative Implementation

```python
class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, data):
        """
        the append method will insert an element at the end of the linked list. 
        """
        new_node = Node(data)
        
        if not self.head:  # the linked list is empty
            self.head = new_node
            return
        
        last_node = self.head  # the linked list is not empty
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
        
    def prepend(self, data):
        """
        the prepend method will insert an element at the beginning of the linked list.
        """
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        
    def insert_after_node(self, pre_node, data):
        """
        this method will insert an element after a given node.
        """
        if not pre_node:
            print("Previous node is None")
            return
        
        new_node = Node(data)
        new_node.next = pre_node.next
        pre_node.next = new_node
        
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
            
    def delete_node_at_pos(self, pos):
        """
        it will delete a node based on given position. 
        """
        cur_node = self.head
        if cur_node and pos == 0:
            self.head = cur_node.next
            cur_node = None
        
        count = 0
        pre_node = None
        while cur_node and count != pos:
            pre_node = cur_node
            cur_node = cur_node.next
            count += 1
        if not cur_node: return
        pre_node.next = cur_node.next
        cur_node = None
    
    def print_list(self):
        """
        this method will print out the data component of the node from the head node to the last node.
        """
        cur_node = self.head
        while cur_node:
            print(cur_node.data)
            cur_node = cur_node.next
    
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

##### 4-2). Recursive Implementation

For any recursive method, we need a base case. In this class, the base case is whether or not we've encountered the end of the linked list.
- if we reach the end of the linked list, meaning the node is `None`, we should return `0`, otherwise;
- if the node is not `None`, we call the recursive method and pass in the next node, finally return 1 plus what we are goning to return from the recursive result. 



```python
class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, data):
        """
        the append method will insert an element at the end of the linked list. 
        """
        new_node = Node(data)
        
        if not self.head:  # the linked list is empty
            self.head = new_node
            return
        
        last_node = self.head  # the linked list is not empty
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
        
    def prepend(self, data):
        """
        the prepend method will insert an element at the beginning of the linked list.
        """
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        
    def insert_after_node(self, pre_node, data):
        """
        this method will insert an element after a given node.
        """
        if not pre_node:
            print("Previous node is None")
            return
        
        new_node = Node(data)
        new_node.next = pre_node.next
        pre_node.next = new_node
        
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
            
    def delete_node_at_pos(self, pos):
        """
        it will delete a node based on given position. 
        """
        cur_node = self.head
        if cur_node and pos == 0:
            self.head = cur_node.next
            cur_node = None
        
        count = 0
        pre_node = None
        while cur_node and count != pos:
            pre_node = cur_node
            cur_node = cur_node.next
            count += 1
        if not cur_node: return
        pre_node.next = cur_node.next
        cur_node = None
    
    def print_list(self):
        """
        this method will print out the data component of the node from the head node to the last node.
        """
        cur_node = self.head
        while cur_node:
            print(cur_node.data)
            cur_node = cur_node.next
    
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
    
    def len_recursive(self, node):
        """
        return the number of nodes in a linked list, using recursive method
        """
        if not node: return 0
        return 1 + self.len_recursive(node.next)
```


```python
llist = LinkedList()
print("The length of an empty linked list is:")
print(llist.len_recursive(llist.head))
llist.append("A")
llist.append("B")
llist.append("C")
llist.append("D")

print("The length of the linked list calculated recursively after inserting 4 elements is:")
print(llist.len_recursive(llist.head))
print("The length of the linked list calculated iteratively after inserting 4 elements is:")
print(llist.len_iterative())
```

    The length of an empty linked list is:
    0
    The length of the linked list calculated recursively after inserting 4 elements is:
    4
    The length of the linked list calculated iteratively after inserting 4 elements is:
    4


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


```python
class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, data):
        """
        the append method will insert an element at the end of the linked list. 
        """
        new_node = Node(data)
        
        if not self.head:  # the linked list is empty
            self.head = new_node
            return
        
        last_node = self.head  # the linked list is not empty
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
        
    def prepend(self, data):
        """
        the prepend method will insert an element at the beginning of the linked list.
        """
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        
    def insert_after_node(self, pre_node, data):
        """
        this method will insert an element after a given node.
        """
        if not pre_node:
            print("Previous node is None")
            return
        
        new_node = Node(data)
        new_node.next = pre_node.next
        pre_node.next = new_node
        
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
            
    def delete_node_at_pos(self, pos):
        """
        it will delete a node based on given position. 
        """
        cur_node = self.head
        if cur_node and pos == 0:
            self.head = cur_node.next
            cur_node = None
        
        count = 0
        pre_node = None
        while cur_node and count != pos:
            pre_node = cur_node
            cur_node = cur_node.next
            count += 1
        if not cur_node: return
        pre_node.next = cur_node.next
        cur_node = None
    
    def print_list(self):
        """
        this method will print out the data component of the node from the head node to the last node.
        """
        cur_node = self.head
        while cur_node:
            print(cur_node.data)
            cur_node = cur_node.next
    
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
    
    def len_recursive(self, node):
        """
        return the number of nodes in a linked list, using recursive method
        """
        if not node: return 0
        return 1 + self.len_recursive(node.next)
    
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
            pre_2.next = cur_1
        else:    # data_2 is the head node
            self.head = cur_1

        cur_2.next, cur_1.next = cur_1.next, cur_2.next    # swap the two nodes.
    
```


```python
llist = LinkedList()
llist.append("A")
llist.append("B")
llist.append("C")
llist.append("D")

print("Original List")
llist.print_list()


llist.swap_nodes("B", "C")
print("Swapping nodes B and C that are not head nodes")
llist.print_list()

llist.swap_nodes("A", "B")
print("Swapping nodes A and B where key_1 is head node")
llist.print_list()

llist.swap_nodes("D", "B")
print("Swapping nodes D and B where key_2 is head node")
llist.print_list()

llist.swap_nodes("C", "C")
print("Swapping nodes C and C where both keys are same")
llist.print_list()
```

    Original List
    A
    B
    C
    D
    Swapping nodes B and C that are not head nodes
    A
    C
    B
    D
    Swapping nodes A and B where key_1 is head node
    B
    C
    A
    D
    Swapping nodes D and B where key_2 is head node
    D
    C
    A
    B
    Swapping nodes C and C where both keys are same
    D
    C
    A
    B


#### 6). Reverse 

Now, we learn how to reverse a singly linked list in an `iterative` way and a `recursive` way. Before getting started, let's know how to reverse a linked list first.

<img src="/Users/caoweiwei/Library/Application Support/typora-user-images/image-20191218170049176.png" alt="image-20191218170049176" style="zoom:33%;" />

##### 6-1). Iterative implementation
The key idea is that we’re reversing the orientation of the arrows. For example, node A is initially pointing to node B but after we flip them, node B points to node A. The same is the case for other nodes. 


```python
class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, data):
        """
        the append method will insert an element at the end of the linked list. 
        """
        new_node = Node(data)
        
        if not self.head:  # the linked list is empty
            self.head = new_node
            return
        
        last_node = self.head  # the linked list is not empty
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
        
    def prepend(self, data):
        """
        the prepend method will insert an element at the beginning of the linked list.
        """
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        
    def insert_after_node(self, pre_node, data):
        """
        this method will insert an element after a given node.
        """
        if not pre_node:
            print("Previous node is None")
            return
        
        new_node = Node(data)
        new_node.next = pre_node.next
        pre_node.next = new_node
        
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
            
    def delete_node_at_pos(self, pos):
        """
        it will delete a node based on given position. 
        """
        cur_node = self.head
        if cur_node and pos == 0:
            self.head = cur_node.next
            cur_node = None
        
        count = 0
        pre_node = None
        while cur_node and count != pos:
            pre_node = cur_node
            cur_node = cur_node.next
            count += 1
        if not cur_node: return
        pre_node.next = cur_node.next
        cur_node = None
    
    def print_list(self):
        """
        this method will print out the data component of the node from the head node to the last node.
        """
        cur_node = self.head
        while cur_node:
            print(cur_node.data)
            cur_node = cur_node.next
    
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
    
    def len_recursive(self, node):
        """
        return the number of nodes in a linked list, using recursive method
        """
        if not node: return 0
        return 1 + self.len_recursive(node.next)
    
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
            pre_2.next = cur_1
        else:    # data_2 is the head node
            self.head = cur_1

        cur_2.next, cur_1.next = cur_1.next, cur_2.next    # swap the two nodes.
        
    def reverse_iterative(self):
        """
        it will reverse the linked list, using iterative method
        """
        pre, cur = None, self.head
        while cur:  # fipping each node's pointer
            nxt = cur.next
            cur.next = pre
            pre = cur
            cur = nxt
        
        self.head = pre    # finally, the last node is pre
    
```


```python
llist = LinkedList()
llist.append("A")
llist.append("B")
llist.append("C")
llist.append("D")
print("Before reversing:")
llist.print_list()

llist.reverse_iterative()
print("After reversing:")

llist.print_list()
```

    Before reversing:
    A
    B
    C
    D
    After reversing:
    D
    C
    B
    A


##### 6-2). Recursive Implementation

The crux of recursive solution is as follows:
- the base case;
- assume we solve the simplest problem, which in this case is to reverse just ONE pair of nodes
- the rest nodes of the linked list will repeat above process.



```python
class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, data):
        """
        the append method will insert an element at the end of the linked list. 
        """
        new_node = Node(data)
        
        if not self.head:  # the linked list is empty
            self.head = new_node
            return
        
        last_node = self.head  # the linked list is not empty
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
        
    def prepend(self, data):
        """
        the prepend method will insert an element at the beginning of the linked list.
        """
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        
    def insert_after_node(self, pre_node, data):
        """
        this method will insert an element after a given node.
        """
        if not pre_node:
            print("Previous node is None")
            return
        
        new_node = Node(data)
        new_node.next = pre_node.next
        pre_node.next = new_node
        
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
            
    def delete_node_at_pos(self, pos):
        """
        it will delete a node based on given position. 
        """
        cur_node = self.head
        if cur_node and pos == 0:
            self.head = cur_node.next
            cur_node = None
        
        count = 0
        pre_node = None
        while cur_node and count != pos:
            pre_node = cur_node
            cur_node = cur_node.next
            count += 1
        if not cur_node: return
        pre_node.next = cur_node.next
        cur_node = None
    
    def print_list(self):
        """
        this method will print out the data component of the node from the head node to the last node.
        """
        cur_node = self.head
        while cur_node:
            print(cur_node.data)
            cur_node = cur_node.next
    
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
    
    def len_recursive(self, node):
        """
        return the number of nodes in a linked list, using recursive method
        """
        if not node: return 0
        return 1 + self.len_recursive(node.next)
    
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
            pre_2.next = cur_1
        else:    # data_2 is the head node
            self.head = cur_1

        cur_2.next, cur_1.next = cur_1.next, cur_2.next    # swap the two nodes.
        
    def reverse_iterative(self):
        """
        it will reverse the linked list, using iterative method
        """
        pre, cur = None, self.head
        while cur:  # fipping each node's pointer
            nxt = cur.next
            cur.next = pre
            pre = cur
            cur = nxt
        
        self.head = pre    # finally, the last node is pre
    
    def reverse_recursive(self):
        """
        it will reverse the linked list, using recursive method
        """
        def _reverse_recursive(cur, pre):
            if not cur:    # base case, the lase node cur is empty, we return pre
                return pre
            
            nxt = cur.next    # using cur and pre filpe the pointer
            cur.next = pre
            pre = cur
            cur = nxt
            return _reverse_recursive(cur, pre)
        
        self.head = _reverse_recursive(cur=self.head, pre=None)    # setting the head, which is the pre
```


```python
llist = LinkedList()
llist.append("1")
llist.append("2")
llist.append("3")
llist.append("4")
print("Before reversing:")
llist.print_list()

llist.reverse_iterative()
print("After reversing:")

llist.print_list()
```

    Before reversing:
    1
    2
    3
    4
    After reversing:
    4
    3
    2
    1


#### 7). Merge Two Sorted Linked Lists

Now, we have another linked list which is sorted, we want it insert into the linked list while keepping the final linked list sorted as well(we will do this in-place), the basic ideas as follows:
- the given two linked list must be sorted;
- two pointers p and q which will initially point to the head node of each linked list;
- pointer s will point to the smaller value of data of the nodes that p and p are pointing to;
- first is to get the new head, like a dummy node used before, then using s to keep track the smaller one while p and q are not empty;
- then if one p and q is empty, then append the other one to the s


```python
class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, data):
        """
        the append method will insert an element at the end of the linked list. 
        """
        new_node = Node(data)
        
        if not self.head:  # the linked list is empty
            self.head = new_node
            return
        
        last_node = self.head  # the linked list is not empty
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
        
    def prepend(self, data):
        """
        the prepend method will insert an element at the beginning of the linked list.
        """
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        
    def insert_after_node(self, pre_node, data):
        """
        this method will insert an element after a given node.
        """
        if not pre_node:
            print("Previous node is None")
            return
        
        new_node = Node(data)
        new_node.next = pre_node.next
        pre_node.next = new_node
        
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
            
    def delete_node_at_pos(self, pos):
        """
        it will delete a node based on given position. 
        """
        cur_node = self.head
        if cur_node and pos == 0:
            self.head = cur_node.next
            cur_node = None
        
        count = 0
        pre_node = None
        while cur_node and count != pos:
            pre_node = cur_node
            cur_node = cur_node.next
            count += 1
        if not cur_node: return
        pre_node.next = cur_node.next
        cur_node = None
    
    def print_list(self):
        """
        this method will print out the data component of the node from the head node to the last node.
        """
        cur_node = self.head
        while cur_node:
            print(cur_node.data)
            cur_node = cur_node.next
    
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
    
    def len_recursive(self, node):
        """
        return the number of nodes in a linked list, using recursive method
        """
        if not node: return 0
        return 1 + self.len_recursive(node.next)
    
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
            pre_2.next = cur_1
        else:    # data_2 is the head node
            self.head = cur_1

        cur_2.next, cur_1.next = cur_1.next, cur_2.next    # swap the two nodes.
        
    def reverse_iterative(self):
        """
        it will reverse the linked list, using iterative method
        """
        pre, cur = None, self.head
        while cur:  # fipping each node's pointer
            nxt = cur.next
            cur.next = pre
            pre = cur
            cur = nxt
        
        self.head = pre    # finally, the last node is pre
    
    def reverse_recursive(self):
        """
        it will reverse the linked list, using recursive method
        """
        def _reverse_recursive(cur, pre):
            if not cur:    # base case, the lase node cur is empty, we return pre
                return pre
            
            nxt = cur.next    # using cur and pre filpe the pointer
            cur.next = pre
            pre = cur
            cur = nxt
            return _reverse_recursive(cur, pre)
        
        self.head = _reverse_recursive(cur=self.head, pre=None)    # setting the head, which is the pre
        
    def merge_sorted(self, llist):
        """
        it will merge llist into the linked list, return a new head of the merged linked list
        """
        p, q = self.head, llist.head
        if not p: return q    # if one of the linked list is empty, then return another
        if not q: return p
        
        if p.data <= q.data:    # this step is to make a head_node, like making dummy
            s = p
            p = p.next
        else:
            s = q
            q = q.next
        new_head = s
        while p and q:    # this is the key process for merging two linked lists
            if p.data < q.data:
                s.next = p
                s = p
                p = p.next
            else:
                s.next = q
                s = q
                q = q.next
        if not p: s.next = q
        if not q: s.next = p
        
        return new_head
    
```


```python
llist_1 = LinkedList()
llist_2 = LinkedList()

llist_1.append(1)
llist_1.append(5)
llist_1.append(7)
llist_1.append(9)
llist_1.append(10)
print("llist_1: ")
llist_1.print_list()

llist_2.append(2)
llist_2.append(3)
llist_2.append(4)
llist_2.append(6)
llist_2.append(8)
print("llist_2: ")
llist_2.print_list()

print("llist_1 merge llist_2: ")
llist_1.merge_sorted(llist_2)
llist_1.print_list()
```

    llist_1: 
    1
    5
    7
    9
    10
    llist_2: 
    2
    3
    4
    6
    8
    llist_1 merge llist_2: 
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10


#### 8). Remove Duplicates

We use a hash-table or dictionary in Python to remove all duplicate entries from a single linked list.

- The general approach to solve this problem is to loop through the linked list once and keep track of all the data held at each of the nodes.  
- Use a dictionary to keep track of the data elements that we encounter to determine whether in the dictionary.


```python
class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, data):
        """
        the append method will insert an element at the end of the linked list. 
        """
        new_node = Node(data)
        
        if not self.head:  # the linked list is empty
            self.head = new_node
            return
        
        last_node = self.head  # the linked list is not empty
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
        
    def prepend(self, data):
        """
        the prepend method will insert an element at the beginning of the linked list.
        """
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        
    def insert_after_node(self, pre_node, data):
        """
        this method will insert an element after a given node.
        """
        if not pre_node:
            print("Previous node is None")
            return
        
        new_node = Node(data)
        new_node.next = pre_node.next
        pre_node.next = new_node
        
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
            
    def delete_node_at_pos(self, pos):
        """
        it will delete a node based on given position. 
        """
        cur_node = self.head
        if cur_node and pos == 0:
            self.head = cur_node.next
            cur_node = None
        
        count = 0
        pre_node = None
        while cur_node and count != pos:
            pre_node = cur_node
            cur_node = cur_node.next
            count += 1
        if not cur_node: return
        pre_node.next = cur_node.next
        cur_node = None
    
    def print_list(self):
        """
        this method will print out the data component of the node from the head node to the last node.
        """
        cur_node = self.head
        while cur_node:
            print(cur_node.data)
            cur_node = cur_node.next
    
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
    
    def len_recursive(self, node):
        """
        return the number of nodes in a linked list, using recursive method
        """
        if not node: return 0
        return 1 + self.len_recursive(node.next)
    
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
            pre_2.next = cur_1
        else:    # data_2 is the head node
            self.head = cur_1

        cur_2.next, cur_1.next = cur_1.next, cur_2.next    # swap the two nodes.
        
    def reverse_iterative(self):
        """
        it will reverse the linked list, using iterative method
        """
        pre, cur = None, self.head
        while cur:  # fipping each node's pointer
            nxt = cur.next
            cur.next = pre
            pre = cur
            cur = nxt
        
        self.head = pre    # finally, the last node is pre
    
    def reverse_recursive(self):
        """
        it will reverse the linked list, using recursive method
        """
        def _reverse_recursive(cur, pre):
            if not cur:    # base case, the lase node cur is empty, we return pre
                return pre
            
            nxt = cur.next    # using cur and pre filpe the pointer
            cur.next = pre
            pre = cur
            cur = nxt
            return _reverse_recursive(cur, pre)
        
        self.head = _reverse_recursive(cur=self.head, pre=None)    # setting the head, which is the pre
        
    def merge_sorted(self, llist):
        """
        it will merge llist into the linked list, return a new head of the merged linked list
        """
        p, q = self.head, llist.head
        if not p: return q    # if one of the linked list is empty, then return another
        if not q: return p
        
        if p.data <= q.data:    # this step is to make a head_node, like making dummy
            s = p
            p = p.next
        else:
            s = q
            q = q.next
        new_head = s
        while p and q:    # this is the key process for merging two linked lists
            if p.data < q.data:
                s.next = p
                s = p
                p = p.next
            else:
                s.next = q
                s = q
                q = q.next
        if not p: s.next = q
        if not q: s.next = p
        
        return new_head
    
    def remove_duplicates(self):
        """
        it will remove duplicate data held by nodes, using a dictionary.
        """
        dup_data = dict()
        cur = self.head
        pre = None
        while cur:
            if cur.data in dup_data:    # if the data has existed in the dictionary, then prepare for removing it
                pre.next = cur.next
                cur = None
            else:
                dup_data[cur.data] = 1  # else, put the data in the dictionary
                pre = cur
            cur = pre.next    # this pre.next is good
        
```


```python
llist = LinkedList()
llist.append(1)
llist.append(6)
llist.append(1)
llist.append(4)
llist.append(2)
llist.append(2)
llist.append(4)

print("Original Linked List")
llist.print_list()
print("Linked List After Removing Duplicates")
llist.remove_duplicates()
llist.print_list()

```

    Original Linked List
    1
    6
    1
    4
    2
    2
    4
    Linked List After Removing Duplicates
    1
    6
    4
    2


#### 9). Nth-from-last Nodes

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


```python
class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, data):
        """
        the append method will insert an element at the end of the linked list. 
        """
        new_node = Node(data)
        
        if not self.head:  # the linked list is empty
            self.head = new_node
            return
        
        last_node = self.head  # the linked list is not empty
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
        
    def prepend(self, data):
        """
        the prepend method will insert an element at the beginning of the linked list.
        """
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        
    def insert_after_node(self, pre_node, data):
        """
        this method will insert an element after a given node.
        """
        if not pre_node:
            print("Previous node is None")
            return
        
        new_node = Node(data)
        new_node.next = pre_node.next
        pre_node.next = new_node
        
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
            
    def delete_node_at_pos(self, pos):
        """
        it will delete a node based on given position. 
        """
        cur_node = self.head
        if cur_node and pos == 0:
            self.head = cur_node.next
            cur_node = None
        
        count = 0
        pre_node = None
        while cur_node and count != pos:
            pre_node = cur_node
            cur_node = cur_node.next
            count += 1
        if not cur_node: return
        pre_node.next = cur_node.next
        cur_node = None
    
    def print_list(self):
        """
        this method will print out the data component of the node from the head node to the last node.
        """
        cur_node = self.head
        while cur_node:
            print(cur_node.data)
            cur_node = cur_node.next
    
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
    
    def len_recursive(self, node):
        """
        return the number of nodes in a linked list, using recursive method
        """
        if not node: return 0
        return 1 + self.len_recursive(node.next)
    
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
            pre_2.next = cur_1
        else:    # data_2 is the head node
            self.head = cur_1

        cur_2.next, cur_1.next = cur_1.next, cur_2.next    # swap the two nodes.
        
    def reverse_iterative(self):
        """
        it will reverse the linked list, using iterative method
        """
        pre, cur = None, self.head
        while cur:  # fipping each node's pointer
            nxt = cur.next
            cur.next = pre
            pre = cur
            cur = nxt
        
        self.head = pre    # finally, the last node is pre
    
    def reverse_recursive(self):
        """
        it will reverse the linked list, using recursive method
        """
        def _reverse_recursive(cur, pre):
            if not cur:    # base case, the lase node cur is empty, we return pre
                return pre
            
            nxt = cur.next    # using cur and pre filpe the pointer
            cur.next = pre
            pre = cur
            cur = nxt
            return _reverse_recursive(cur, pre)
        
        self.head = _reverse_recursive(cur=self.head, pre=None)    # setting the head, which is the pre
        
    def merge_sorted(self, llist):
        """
        it will merge llist into the linked list, return a new head of the merged linked list
        """
        p, q = self.head, llist.head
        if not p: return q    # if one of the linked list is empty, then return another
        if not q: return p
        
        if p.data <= q.data:    # this step is to make a head_node, like making dummy
            s = p
            p = p.next
        else:
            s = q
            q = q.next
        new_head = s
        while p and q:    # this is the key process for merging two linked lists
            if p.data < q.data:
                s.next = p
                s = p
                p = p.next
            else:
                s.next = q
                s = q
                q = q.next
        if not p: s.next = q
        if not q: s.next = p
        
        return new_head
    
    def remove_duplicates(self):
        """
        it will remove duplicate data held by nodes, using a dictionary.
        """
        dup_data = dict()
        cur = self.head
        pre = None
        while cur:
            if cur.data in dup_data:    # if the data has existed in the dictionary, then prepare for removing it
                pre.next = cur.next
                cur = None
            else:
                dup_data[cur.data] = 1  # else, put the data in the dictionary
                pre = cur
            cur = pre.next    # this pre.next is good
    
    def print_nth_from_last(self, n, method):
        """
        to find out the data of n-th node from the last
        - using parameter 1 choosing two pointer solution,
        - using parameter 2 choosing length based solution,
        """
        if method == 1:
            p = q = self.head
            
            count = 0
            while q:
                count += 1
                if count >= n: break
                q = q.next
            
            if not q: 
                print(str(n) + "is greater than the length of the linked list.")
                return None
            
            while p and q.next:
                p = p.next
                q = q.next
            
            return p.data
        
        elif method == 2:
            total_len = self.len_iterative()
            cur = self.head
            
            while cur:
                if total_len == n:
                    return cur.data
                total_len -= 1
                cur = cur.next
            
            if not cur:
                print(str(n) + "is greater than the length of the linked list.")
                return None
```


```python
llist = LinkedList()
llist.append("A")
llist.append("B")
llist.append("C")
llist.append("D")
llist.append("E")

print(llist.print_nth_from_last(2,1))
print(llist.print_nth_from_last(2,2))
```

    D
    D


#### 10). Count Occurrences

Now we will investigate how to count the occurrence of nodes with a specifited element. And solutions will be implemented both in iterative and recursive.

1. Iterative solution

It's very straightforward, just using a variable to count the frequency of the given data element when loop through the linked list.


```python
def count_occurences_iterative(self, data):
    """
    to count the occurrence of nodes with a specified data element, using iterative solution
    """
    cur = self.head
    count = 0
    while cur:
        if cur.data == data:
            count += 1
        cur = cur.next
    return count
```

Another way is recursion, here is the main idea:
- if the current node's data equals to the given data, then we count 1 and recursivelly call the method passing next node of the current node
- else, we just call the method passing the next node
- the base case is the node is empty, we return 0 since there is nothing.

A better way to understand recursive solution is drawing recursive tree whenever you try to use a recursive solution.


```python
def count_occurences_recursive(self, node, data):
    """
    to count the occurence of nodes with a specified data element, using recursive solution
    """
    if not cur: return 0
    if node.data == data: 
        return 1 + self.count_occurences_recursive(node.next, data)
    else: 
        return self.count_occurences_recursive(node.next, data)
```


```python
class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, data):
        """
        the append method will insert an element at the end of the linked list. 
        """
        new_node = Node(data)
        
        if not self.head:  # the linked list is empty
            self.head = new_node
            return
        
        last_node = self.head  # the linked list is not empty
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
        
    def prepend(self, data):
        """
        the prepend method will insert an element at the beginning of the linked list.
        """
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        
    def insert_after_node(self, pre_node, data):
        """
        this method will insert an element after a given node.
        """
        if not pre_node:
            print("Previous node is None")
            return
        
        new_node = Node(data)
        new_node.next = pre_node.next
        pre_node.next = new_node
        
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
            
    def delete_node_at_pos(self, pos):
        """
        it will delete a node based on given position. 
        """
        cur_node = self.head
        if cur_node and pos == 0:
            self.head = cur_node.next
            cur_node = None
        
        count = 0
        pre_node = None
        while cur_node and count != pos:
            pre_node = cur_node
            cur_node = cur_node.next
            count += 1
        if not cur_node: return
        pre_node.next = cur_node.next
        cur_node = None
    
    def print_list(self):
        """
        this method will print out the data component of the node from the head node to the last node.
        """
        cur_node = self.head
        while cur_node:
            print(cur_node.data)
            cur_node = cur_node.next
    
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
    
    def len_recursive(self, node):
        """
        return the number of nodes in a linked list, using recursive method
        """
        if not node: return 0
        return 1 + self.len_recursive(node.next)
    
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
            pre_2.next = cur_1
        else:    # data_2 is the head node
            self.head = cur_1

        cur_2.next, cur_1.next = cur_1.next, cur_2.next    # swap the two nodes.
        
    def reverse_iterative(self):
        """
        it will reverse the linked list, using iterative method
        """
        pre, cur = None, self.head
        while cur:  # fipping each node's pointer
            nxt = cur.next
            cur.next = pre
            pre = cur
            cur = nxt
        
        self.head = pre    # finally, the last node is pre
    
    def reverse_recursive(self):
        """
        it will reverse the linked list, using recursive method
        """
        def _reverse_recursive(cur, pre):
            if not cur:    # base case, the lase node cur is empty, we return pre
                return pre
            
            nxt = cur.next    # using cur and pre filpe the pointer
            cur.next = pre
            pre = cur
            cur = nxt
            return _reverse_recursive(cur, pre)
        
        self.head = _reverse_recursive(cur=self.head, pre=None)    # setting the head, which is the pre
        
    def merge_sorted(self, llist):
        """
        it will merge llist into the linked list, return a new head of the merged linked list
        """
        p, q = self.head, llist.head
        if not p: return q    # if one of the linked list is empty, then return another
        if not q: return p
        
        if p.data <= q.data:    # this step is to make a head_node, like making dummy
            s = p
            p = p.next
        else:
            s = q
            q = q.next
        new_head = s
        while p and q:    # this is the key process for merging two linked lists
            if p.data < q.data:
                s.next = p
                s = p
                p = p.next
            else:
                s.next = q
                s = q
                q = q.next
        if not p: s.next = q
        if not q: s.next = p
        
        return new_head
    
    def remove_duplicates(self):
        """
        it will remove duplicate data held by nodes, using a dictionary.
        """
        dup_data = dict()
        cur = self.head
        pre = None
        while cur:
            if cur.data in dup_data:    # if the data has existed in the dictionary, then prepare for removing it
                pre.next = cur.next
                cur = None
            else:
                dup_data[cur.data] = 1  # else, put the data in the dictionary
                pre = cur
            cur = pre.next    # this pre.next is good
    
    def print_nth_from_last(self, n, method):
        """
        to find out the data of n-th node from the last
        - using parameter 1 choosing two pointer solution,
        - using parameter 2 choosing length based solution,
        """
        if method == 1:
            p = q = self.head
            
            count = 0
            while q:
                count += 1
                if count >= n: break
                q = q.next
            
            if not q: 
                print(str(n) + "is greater than the length of the linked list.")
                return None
            
            while p and q.next:
                p = p.next
                q = q.next
            
            return p.data
        
        elif method == 2:
            total_len = self.len_iterative()
            cur = self.head
            
            while cur:
                if total_len == n:
                    return cur.data
                total_len -= 1
                cur = cur.next
            
            if not cur:
                print(str(n) + "is greater than the length of the linked list.")
                return None
        
    def count_occurences_iterative(self, data):
        """
        to count the occurrence of nodes with a specified data element, using iterative solution
        """
        cur = self.head
        count = 0
        while cur:
            if cur.data == data:
                count += 1
            cur = cur.next
        return count

    def count_occurences_recursive(self, node, data):
        """
        to count the occurence of nodes with a specified data element, using recursive solution
        """
        if not node: return 0
        if node.data == data: 
            return 1 + self.count_occurences_recursive(node.next, data)
        else: 
            return self.count_occurences_recursive(node.next, data)

```


```python
llist = LinkedList()
llist.append(1)
llist.append(2)
llist.append(3)
llist.append(4)
llist.append(5)
llist.append(6)

llist_2 = LinkedList()
llist_2.append(1)
llist_2.append(2)
llist_2.append(1)
llist_2.append(3)
llist_2.append(1)
llist_2.append(4)
llist_2.append(1)
print(llist_2.count_occurences_iterative(1))
print(llist_2.count_occurences_recursive(llist_2.head, 1))
```

    4
    4


#### 11). Rotate

Now, let'st learn how to rotate the nodes of a singly linked list around **a specified pivot element**. This implies shifting or rotating everything that follows the pivot node to the front of the linked list.

The algorithm as follows:

<img src="/Users/caoweiwei/Library/Application Support/typora-user-images/image-20191218170302932.png" alt="image-20191218170302932" style="zoom:33%;" />

- Make use of two pointers `p` and `q`, `p` points to the pivot node while `q` points to the end of the linked list.
- Then make `q.next` point to the head of the linked list to achieve a circular linked list
- And, update the head of the linked list, which will be the next element after the pivot node
- Finally,set `p.next` to `None` which breaks up the circular linked list.



```python
def rotate(self, k):
    """
    rotate the linked list around the k-th node
    """
    if self.head and self.head.next:
        p = q = self.head
        count = 1
        while p and count < k:
            p = p.next
            count += 1
        q = p
        while q.next:
            q = q.next

        q.next = self.head
        self.head = p.next
        p.next = None
    
```


```python
class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, data):
        """
        the append method will insert an element at the end of the linked list. 
        """
        new_node = Node(data)
        
        if not self.head:  # the linked list is empty
            self.head = new_node
            return
        
        last_node = self.head  # the linked list is not empty
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
        
    def prepend(self, data):
        """
        the prepend method will insert an element at the beginning of the linked list.
        """
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        
    def insert_after_node(self, pre_node, data):
        """
        this method will insert an element after a given node.
        """
        if not pre_node:
            print("Previous node is None")
            return
        
        new_node = Node(data)
        new_node.next = pre_node.next
        pre_node.next = new_node
        
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
            
    def delete_node_at_pos(self, pos):
        """
        it will delete a node based on given position. 
        """
        cur_node = self.head
        if cur_node and pos == 0:
            self.head = cur_node.next
            cur_node = None
        
        count = 0
        pre_node = None
        while cur_node and count != pos:
            pre_node = cur_node
            cur_node = cur_node.next
            count += 1
        if not cur_node: return
        pre_node.next = cur_node.next
        cur_node = None
    
    def print_list(self):
        """
        this method will print out the data component of the node from the head node to the last node.
        """
        cur_node = self.head
        while cur_node:
            print(cur_node.data)
            cur_node = cur_node.next
    
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
    
    def len_recursive(self, node):
        """
        return the number of nodes in a linked list, using recursive method
        """
        if not node: return 0
        return 1 + self.len_recursive(node.next)
    
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
            pre_2.next = cur_1
        else:    # data_2 is the head node
            self.head = cur_1

        cur_2.next, cur_1.next = cur_1.next, cur_2.next    # swap the two nodes.
        
    def reverse_iterative(self):
        """
        it will reverse the linked list, using iterative method
        """
        pre, cur = None, self.head
        while cur:  # fipping each node's pointer
            nxt = cur.next
            cur.next = pre
            pre = cur
            cur = nxt
        
        self.head = pre    # finally, the last node is pre
    
    def reverse_recursive(self):
        """
        it will reverse the linked list, using recursive method
        """
        def _reverse_recursive(cur, pre):
            if not cur:    # base case, the lase node cur is empty, we return pre
                return pre
            
            nxt = cur.next    # using cur and pre filpe the pointer
            cur.next = pre
            pre = cur
            cur = nxt
            return _reverse_recursive(cur, pre)
        
        self.head = _reverse_recursive(cur=self.head, pre=None)    # setting the head, which is the pre
        
    def merge_sorted(self, llist):
        """
        it will merge llist into the linked list, return a new head of the merged linked list
        """
        p, q = self.head, llist.head
        if not p: return q    # if one of the linked list is empty, then return another
        if not q: return p
        
        if p.data <= q.data:    # this step is to make a head_node, like making dummy
            s = p
            p = p.next
        else:
            s = q
            q = q.next
        new_head = s
        while p and q:    # this is the key process for merging two linked lists
            if p.data < q.data:
                s.next = p
                s = p
                p = p.next
            else:
                s.next = q
                s = q
                q = q.next
        if not p: s.next = q
        if not q: s.next = p
        
        return new_head
    
    def remove_duplicates(self):
        """
        it will remove duplicate data held by nodes, using a dictionary.
        """
        dup_data = dict()
        cur = self.head
        pre = None
        while cur:
            if cur.data in dup_data:    # if the data has existed in the dictionary, then prepare for removing it
                pre.next = cur.next
                cur = None
            else:
                dup_data[cur.data] = 1  # else, put the data in the dictionary
                pre = cur
            cur = pre.next    # this pre.next is good
    
    def print_nth_from_last(self, n, method):
        """
        to find out the data of n-th node from the last
        - using parameter 1 choosing two pointer solution,
        - using parameter 2 choosing length based solution,
        """
        if method == 1:
            p = q = self.head
            
            count = 0
            while q:
                count += 1
                if count >= n: break
                q = q.next
            
            if not q: 
                print(str(n) + "is greater than the length of the linked list.")
                return None
            
            while p and q.next:
                p = p.next
                q = q.next
            
            return p.data
        
        elif method == 2:
            total_len = self.len_iterative()
            cur = self.head
            
            while cur:
                if total_len == n:
                    return cur.data
                total_len -= 1
                cur = cur.next
            
            if not cur:
                print(str(n) + "is greater than the length of the linked list.")
                return None
        
    def count_occurences_iterative(self, data):
        """
        to count the occurrence of nodes with a specified data element, using iterative solution
        """
        cur = self.head
        count = 0
        while cur:
            if cur.data == data:
                count += 1
            cur = cur.next
        return count

    def count_occurences_recursive(self, node, data):
        """
        to count the occurence of nodes with a specified data element, using recursive solution
        """
        if not node: return 0
        if node.data == data: 
            return 1 + self.count_occurences_recursive(node.next, data)
        else: 
            return self.count_occurences_recursive(node.next, data)
    
    def rotate(self, k):
        """
        rotate the linked list around the k-th node
        """
        if self.head and self.head.next:    # when the linked list is not empty and at least has two items, starting rotate
            p = self.head
            count = 1
            while p and count < k:
                p = p.next
                count += 1
            q = p    # make use of q pointing to the tail of linked list
            while q.next:
                q = q.next

            q.next = self.head
            self.head = p.next
            p.next = None

```


```python
llist = LinkedList()
llist.append(1)
llist.append(2)
llist.append(3)
llist.append(4)
llist.append(5)
llist.append(6)

llist.rotate(2)
llist.print_list()
```

    3
    4
    5
    6
    1
    2


#### 12). Is Palindrome

What is palindrome? If the data held at each of the nodes in the linked list can be read forward from the head or backward from the tail to generate the same content. 

For instance, racecar and radar are palindromes. Examples of non-palindromes are ABC, hello, and test.

For this lesson, we’ll solve the Is Palindrome problem in Python by using three solutions.

##### 12-1). Solution 1: Using a string
the basic idea is that store each data in a string and compare the string whether is equivalent to the reverse of itself.


```python
def is_palindrome(self):
    """
    this solution is based on string methods
    """
    s = ""
    p = self.head
    while p:
        s += p.data
        p = p.next
    return s == s[::-1]    # check if s is equivalent to the reverse of s and returns True or False accordingly.
```

##### 12-2). Solution 2: Using a stack

it's very easy to come upon with using stack to solve this problem. The spirit is similar with solution 1, storing all data in a stack, ans popping each data from the stack comparing with the linked list data.

DON NOT THINK USING MIDDLE NODE, IT MAKES MORE COMPLEX;


```python
def is_palindrome(self):
    """
    this is solution based on using stack
    """
    stack = []
    p = self.head
    while p:
        stack.append(p.data)
        p = p.next
        
    p = self.head
    while p:
        data = stacl.pop()
        if p.data != data: return False
        p = p.next
    
    return True
```

##### 12-3). Solution 3: Using Two Pointers

- list version


```python
def is_palindrome(self):
    if self.head:
        stack = []
        p = q = self.head
        
        i = 0
        while q:    # put each node into a stack so it can traverse backward
            stack.append(q)
            q = q.next
            i += 1

        count = 1
        while count <= i//2 + 1:  # i//2 + 1 is the middle in odd, or middle next in odd
            if stack[-count].data != p.data: return False
            p = p.next
            count += 1
            
        return True
    else:    # [] is palindrome as well, but is will make stack throw error.
        return True
```

- two pointers using reverse method


```python
def is_palindrome(self):
    """
    Using two pointers making the code more concise
    Time: O(n), Space: O(1)
    """
    if not head: return True
    
    slow = fast = head  # finding the middle node of the linked list using slow-fast pointers
    while fast.next and fast.next.next:
        slow = slow.next
        fast = fast.next.next

    def _reverse(cur):  # _method means is a inner method
        pre = None
        while cur:
            nxt = cur.next
            cur.next = pre
            pre = cur
            cur = nxt
        return pre
    new_head = _reverse(slow.next)  # reverse the part is going to be tested
    
    p, q = head, new_head
    while p and q:                  # check whether is or not a palindrome pattern
        if p.data == q.data:
            p = p.next
            q = q.next
        else:
            return False
        
    return True

```


```python

```
