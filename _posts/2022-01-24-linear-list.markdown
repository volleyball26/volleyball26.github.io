---
layout: post
title:  "数据结构-线性表"
date:   2022-01-24 14:13:27 +0800
categories: jekyll update
---
# 线性表
## 定义
线性表是同一类型数据的一个有限序列， 数据之间在逻辑上存在着线性结构。 线性结构是最常用、最简单的一种数据结构，基本特点是有序和有限。这种结构有着一下特点。
1. 存在唯一一个被称为“第一个”的数据元素
2. 存在唯一一个被称为“最后一个”的数据元素
3. 除了第一个元素，每个元素都有一个直接前驱
4. 除了最后一个元素，每个元素都有一个直接后继

线性表的主要存储结构有顺序存储结构和链式存储结构两种。在线性表中，顺序存储结构包括顺序表，链式存储结构包括单链表、双链表、循环链表。

## 顺序表
### 存储结构
把线性表的节点按逻辑顺序依次存放在一组地址连续的存储单元中，用这种方式存储的线性表成为顺序表， 即顺序存储的线性表。
特点：
 - 线性表的逻辑顺序与物理顺序一致
 - 数据元素之间的关系是以元素在计算机内部的“物理位置相邻”来体现的
### 基本操作

```python
class SequenceList:

    def __init__(self, max):
        """[初始化顺序表]

        Args:
            max ([int]): [顺序表长度]
        """
        self.max = max
        self.index = 0
        self.data = [None for _ in range(self.max)]

    def __getitem__(self, index):
        """[获取下标值为index的元素]

        Args:
            index ([int]): [下标]
        """
        if index < 0 or index >= self.index:
            raise IndexError("Index 不合法")
        else:
            return self.data[index]

    def __setitem__(self, index, value):
        """[修改index下标的元素值]

        Args:
        index ([int]): [下标]
        value ([int]): [替换元素]
        """
        if index < 0 or index > self.index:
            raise IndexError("Index 不合法")
        else:
            self.data[index] = value

    def append(self, value):
        """[表尾插入数据]

        Args:
            value ([type]): [description]
        """
        if self.index == self.max:
            return
        else:
            self.data[self.index] = value
            self.index += 1


    def insert(self, index, value):
        """[在任意位置插入元素]

        Args:
            index ([int]): [下标]
            value ([int]): [元素]]
        """
        if index < 0 or index > self.index:
            raise IndexError("Index 不合法")
        if index == self.index:
            self.append(value)
        else:
            for i in range(self.index, index, -1):
                print(i)
                self.data[i] = self.data[i-1]
            self.data[index] = value
            self.index += 1

    def delete(self, index, value):
        """[删除任意位置的元素]

        Args:
            index ([int]): [下标]
            value ([int]): [元素]
        """
        if index < 0 and index > self.index:
            raise IndexError("Index 不合法")
        if index == self.index:
            self.pop()
        for i in range(index, self.index):
            self.data[i] = self.data[i+1]
        self.index -= 1
        

    def pop(self):
        """[删除表尾的元素]
        """
        if self.empty() == True:
            return
        del self.data[-1] 
        self.index -= 1


    def empty(self):
        """[判断顺序表是否为空]

        Returns:
            [Bool]: [返回True 或者 False]
        """
        return True if self.index == 0 else False

    def append(self, value):
        """[表尾插入元素]

        Args:
            value ([int]): [元素]
        """
        if self.index is self.max:
            return
        else:
            self.data[self.index] = value
            self.index += 1

    def length(self):
        """[返回顺序表长度]
        """
        return self.index

    def traversal(self):
        """[遍历顺序表]
        """
        if self.length == 0:
            return
        for i in self.data:
            print(i)

if __name__ == '__main__':
    seq_list = SequenceList(4)
    seq_list.insert(0, 1)
    seq_list.insert(0, 2)
    seq_list.insert(0, 3)
    seq_list.insert(0, 4)

    seq_list.traversal()
```
## 双链表
### 为什么要有双链表
单链表的指向是单向的，如果要访问当前节点的上一个节点，则需要从表头重新开始便利。为了更方便的访问当前节点的前驱节点， 引入了双链表
### 存储结构
双链表就是在单链表的基础上增加了一个指针， 该指针指向前驱节点。这样形成的链表有两个不同方向的链，故称为双链表。

### 基本操作
### 双链表节点定义
```py
class Node:
    def __init__(self, val):
        # 存放节点的数据域
        self.val = val
        # 前驱指针
        self.prev = None
        # 后继指针
        self.next = None
```
### 双链表初始化
```py
class DoubleLinkedList:
    def __init__(self):
        """[双链表初始化]
        """
        # 声明头指针，将头指针指向空
        self.head = None
        # 声明尾指针，将尾指针指向空
        self.tail = None
```
### 判断双链表是否为空
```py
def empty(self):
    return self.head is None
```
### 获取链表长度
```py
def length(self):
    size = 0
    cur = self.head
    while cur != None:
        size += 1
        cur = cur.next
    return size
```
### 头插法
```py
def prepend(self, val):
    """[头部插入]

    Args:
        val ([any]): [插入的值]
    """
    newNode = Node(val)
    if self.empty():
        self.head = newNode
        self.tail = newNode
    else:
        self.head.prev = newNode
        newNode.next = self.head
        self.head = newNode

```
### 任意位置插入数据
```py
def insert(self, index, val):
    """[在链表任意位置添加节点,若该任意位置为index,即在第index个节点后插入元素]

    Args:
        index ([int]): [位置下标]
        val ([any]): [关键字]
    """
    newNode = Node(val)
    # 声明pre指针
    pre = self.head
    # 通过pre指针遍历到链表中第index个节点
    for _ in range(index-1):
        pre = pre.next
    # 第index个节点的后继节点
    node_next = pre.next
    # 将新节点的后继指针指向链表中第index+1个节点
    newNode.next = next
    # 链表中第index+1个节点的前驱指针指向新节点
    node_next.prev = newNode
    # 第index个节点的后继指针指向新节点
    pre.next = newNode
    # 新节点的前驱指针指向链表中第index个节点
    newNode.prev = pre
```
### 删除表头节点
```py
def del_first(self):
    """[删除表头节点]
    """
    if self.empty():
        raise IndexError("下标不合法")
    else:
        self.head = self.head.next
        self.head.prev = None
```
### 删除任意位置节点
```py
def delete(self, index):
    """[删除链表中任意位置节点]

    Args:
        index ([int]): [删除下标为index的结果,表头节点下标为0]
    """
    pre = self.head
    for _ in range(index-1):
        pre = pre.next
    pre.next = pre.next.next
    pre.next.prev = pre
```
### 在链表中查找元素
```py
def find(self, key):
    """[summary]

    Args:
        key ([any]): [关键字key]

    Returns:
        [bool]: [查找结果]
    """
    cur = self.head
    while cur.next != None:
        if cur.val == key:
            return True
        cur = cur.next
    return False
```


## 循环链表
### 存储结构
### 基本操作
```py
```

## 链表的应用
### 存储结构
### 基本操作
```py
```
