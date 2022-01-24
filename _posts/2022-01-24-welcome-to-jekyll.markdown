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
