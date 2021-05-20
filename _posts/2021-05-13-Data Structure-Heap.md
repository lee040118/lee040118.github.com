---
title:  "[Data Structure] 힙(heap)"
excerpt: "힙의 구조를 이해하고 MAX Heap을 구현해 보자"

categories:
  - Data Structure
tags:
  - Data Structure
  - Heap
  - Max Heap
  - C언어
last_modified_at: 2021-05-13T08:06:00-05:00
---

## Goal
> - Heap의 구조를 이해한다.
> - Linked list를 통해 Max Heap을 구현할 수 있다.

## Heap
힙은 우선 순위를 가지는 큐를 효율적으로 구현하기 위해 만들어진 자료구조이다. 

* 우선순위 큐 : 특정한 기준으로 정렬되어 있는 큐 
* ex) 내림차순 , 오름차순, 특정 원소의 크기 기준..

힙은 한 노드가 최대 두개의 자식노드를 가지면서, 마지막 레벨을제외한 모든 레벨에서 노드들이 꽉 채워진 완전이진트리(Complete binary tree)를 기본 특성으로 가진다.

## Heap 종류
* Max heap 
  - 부모 노드의 key값이 자식 노드의 key값 보다 크거나 같은 완전 이진 트리
* Min heap
  - 부모 노드의 key값이 자식 노드의 key값 보다 작거나 같은 완전 이진 트리

## Insertion into a max heap

 1. 힙에 새로운 값이 들어오면, 먼저 새로운 노드를 힙의 마지막 노드에 이어서 삽입힌다.
 2. 새로운 노드를 부모 노드들과 교환하여 힙의 성질을 만족시킨다.
 
 ![enter image description here](/images/Data%20Structure-Heap/insertion%20into%20heap.png)
 
 
 - C언어에서 Max heap 삽입 연산

 `enter code here`


## Heapify
주어진 자료구조에서 힙 성질을 만족하도록 하는 연산을 Heapify라고 한다.

![](/images/Data%20Structure-Heap/heapify.png)


## Deletion from a max heap

 1. heap의 최대값인 root노드에서 삭제 된다.
 2. 삭제된 루트 노드에는 heap이 마지막 노드를 가져온다
 3. 새로운 루트노드와 자식 노드를 비교하면서 바꾸어준다 (root노드의 key값이 가장 커야 한다)
 
 - C언어에서의 Max heap 삭제 연산

    `enter code`

## Time complexity

|  | Unordered linear list | Heap |
|--|:--:|:--:|
| Search(Top) | O(n) | O(1) | 
| Insert(Push) | O(1) | O(log n) |
| Delete(pop) | O(n) | O(log n) |

