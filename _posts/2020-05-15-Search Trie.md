---
layout: default
title: Data Structure - Search Trie in Python
published: 2020-05-15 23:00:00 -0400
comments: true
tags: [Search, Trie, String, Data Structure and Algorithm, Python]
github: "https://github.com/cao-weiwei/"
noimage: true
---



Todaoy, let's check a data structure named `Trie`. It's also called search trie or prefix trie, which is mainly used to handle string related problems. 

<!--more-->

As we known, the balanced binary search tree will give us `O(logN)` time complexity in search/insert/delete, which is efficient. We can use this idea to create a variant of tree, called `Trie`to improve the efficiency of queries in strings, like searching prefix of a word. Trie is very useful in our daily usage of computer like auto complete in search engine.

<img src="/assets/images/posts/Search Trie/01_Trie.png" alt="01_Trie" style="zoom:50%;" />

For example, for words "apple", "ape", "apply", we will pre-process all the characters and save each alphabet in a trie node to form a trie as below:

<img src="/assets/images/posts/Search Trie/00_trie.png" alt="00_trie" style="zoom:50%;" />

As we can see, even "apple" and "apply" are two words, we only store prefix "appl" once. Same prefix of a string will show only once in a `Trie` and this property will help us:

-  to find common prefix by a given string and 
- to get all suffix by a given string efficiently.

For example, suppose we have a `Trie` build by all alphabets, which means the size of each level is `26`. If we want to find a word "book",  we just need to search `26` * `4` times. To be more mathematicly, we can say search in a `Trie` will cost `O(K * M)`, `K` is the size of the alphabet and `M` is the length of given string parameter of the operation.

Next, let's jump onto how to implement this in `Python`.

## Trie Node

Before we design the `Trie`, it's better to give the data structure of trie node. A trie node is to store the data, which holds any additional data associated with the current node and a flag to represent that a word ends at this node.  

```python
class TrieNode:
    def __init__(self):
        """
        Initialize a trie node
        """
        self.data = dict()
        self.is_end = False
```

Now let's look at the previous `Trie` in detail, below is what we will create in Python:

<img src="/assets/images/posts/Search Trie/02_trie-detailed.png" alt="02_trie-detailed" style="zoom:60%;" />

## Trie

During the class `Trie`, we need a root to start operations.

```python
class Trie:
    def __init__(self):
        """
        Initialize a root of a trie
        """
        self.root = TrieNode()
```



### Insertion

The `insert()` method will put a word in the `Tire` and set the flag as `True` which means current   path is representing a complete word.

```python
    def insert(self, word: str) -> None:
        """
        Insert a word into a trie
        :param word: str
        :return: None
        """
        cur_node = self.root
        for w in word:
            if w not in cur_node.data.keys():
                cur_node.data[w] = TrieNode()  # if a character is new to the trie, just append it as a new trie node
            cur_node = cur_node.data.get(w) # else going deeper until at the end of a path
        cur_node.is_end = True
```

### Search

`search()` method will check a word whether in the `Tries`, if existed return `True`, otherwise return `False`. It will go through the dictionary by checking the keys.

```python
    def search(self, word: str) -> bool:
        """
        Search the word whether exists in the trie
        :param word: str
        :return: True if the word exists otherwise False
        """
        cur_node = self.root
        for w in word:
            if w not in cur_node.data.keys():
                return False  # if cur_node doesn't contain this character, which means given word doesn't exist in trie
            cur_node = cur_node.data.get(w)  # going deeper for search the character
        return cur_node.is_end
```



### Check prefix

This method will identify whether the given prefix exist in a `Trie`.

```python
    def start_with(self, prefix: str) -> bool:
        """
        To determine whether there is any word in the trie that starts with the given prefix.
        :param prefix: str
        :return: True if the prefix exists otherwise False
        """
        cur_node = self.root
        for w in prefix:
            if w not in cur_node.data.keys():
                return False
            cur_node = cur_node.data.get(w)
        return True
```



### Auto complete

This is not a strict feature of auto-complete, however it basically implements the key feature which will return a list contains number of words of the given prefix. 

The logic is:

- do some edge cases check first
- then using backtracking techniques to enumerate all possible words

```python
    def auto_complete(self, prefix: str) -> list:
        """
        get all words started with given prefix
        :param prefix: str
        :return: a list of words in the trie that starts with given prefix
        """

        def _get_keys(word: str, node: TrieNode) -> list:
            """
            using backtracking technique to collect all words with given prefix
            :param word: str
            :param node: TrieNode
            :return: a list of words in the trie that starts with given prefix
            """
            word_list = []
            if node.is_end:  # at the end of the search trie, put a word into the answer list
                word_list.append(word)
            for key in node.data.keys():  # go back to traversal all possible paths
                word_list.extend(_get_keys(word + key, node.data.get(key)))
            return word_list

        words = []
        if not self.start_with(prefix):
            # no such prefix in the trie, return empty list
            return words
        elif self.search(prefix):
            # or the prefix is a complete word, just return a list contains the prefix
            words.append(prefix)
            return words
        else:
            # to search all the words in the trie with given prefix
            cur_node = self.root
            for chars in prefix:  # to find the last ancestor in the trie
                cur_node = cur_node.data.get(chars)
            return _get_keys(prefix, cur_node)

```



---

If you like my articles please give me a star or leave comments below, thanks!
