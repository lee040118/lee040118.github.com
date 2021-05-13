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

* 우선순위 큐 : 특정한 기준으로 정렬되어 있는 큐 ex) 내림차순 , 오름차순, 특정 원소의 크기 기준..

힙은 한 노드가 최대 두개의 자식노드를 가지면서, 마지막 레벨을제외한 모든 레벨에서 노드들이 꽉 채워진 완전이진트리(Complete binary tree)를 기본 특성으로 가진다.

## Heapify
주어진 자료구조에서 힙 성질을 만족하도록 하는 연산을 Heapify라고 한다.
![heapify](/images/Data Structure-Heap/heapify.png)
