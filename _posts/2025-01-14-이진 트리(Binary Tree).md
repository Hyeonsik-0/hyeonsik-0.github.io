---
title: 이진 트리(Binary Tree)
date: 2025-01-14 11:14:00 +09:00
last_modified_at: 2025-01-15 11:01:00 +09:00
categories: [Study, DataStructure]
tags:
  [
    이진 트리,
    Binary Tree,
    이진 트리 탐색,
    Binary Tree Traversal,
    이진 탐색 트리,
    Binary Search Tree,
    힙,
    Heap,
    최대 힙,
    최소 힙,
  ]
---
# 이진 트리(Binary Tree)

## 목차

1.  이진 트리의 정의
2.  이진 트리의 성질
3.  이진 트리의 종류
4.  이진 트리의 탐색
    -   DFS
        -   전위 순회(Preorder Traversal)
        -   중위 순회(Inorder Traversal)
        -   후위 순회(Postorder Traversal)
    -   BFS
        -   Level Order Traversal
5.  이진 탐색 트리(Binary Search Tree)
6.  힙(Heap)
    -   최대 힙(Max Heap)
    -   최소 힙(Min Heap)

## 이진 트리의 정의

-   각 노드가 최대 두개의 자식을 갖는 트리
-   재귀적 정의
    -   공백 트리도 이진 트리이다.
    -   T의 자식 트리가 모두 이진 트리이면 T도 이진 트리이다.   

## 이진 트리의 성질

-   레벨 i에서의 최대 노드 수: 2^(i-1) (루트는 레벨 1)
-   깊이가 k일 때 최대 노드 수: 2^k-1   
   
## 이진 트리의 종류

-   완전 이진 트리(Complete Binary Tree)
    -   마지막 레벨을 제외하고 모든 레벨이 노드로 채워져야 함
    -   마지막 레벨의 노드 수는 자유로움
    -   1차원 배열에 저장하면 낭비되는 공간 없이 저장이 가능
-   전 이진 트리(Full Binary Tree)
    -   모든 노드가 0개 또는 2개의 자식 노드를 가짐
    -   단말 노드 수 = 내부 노드 + 1
-   포화 이진 트리(Perfect Binary Tree)
    -   깊이가 k이고 노드 수가 2^k-1개여야 함
    -   완전 이진 트리이면서 전 이진 트리임   
       
## 이진 트리의 탐색

### DFS

-   전위 순회(Preorder Traversal)
    
    ```cpp
    void Preorder(TreeNode *node) { 
      if (node != nullptr) { 
          cout << node->data << " "; 
          preorder(node->leftChild); 
          preorder(node->rightChild); 
      } 
    }
    ```
    
-   중위 순회(Inorder Traversal)
    
    ```cpp
    void Inoder(TreeNode *node) { 
      if (node != nullptr) { 
          Inorder(node->leftChild); 
          cout << node->data << " "; 
          Inorder(node->rightChild); 
      } 
    }
    ```
    
-   후위 순회(Postorder Traversal)
    
    ```cpp
    void Postoder(TreeNode *node) { 
      if (node != nullptr) { 
          Postorder(node->leftChild); 
          Postorder(node->rightChild); 
          cout << node->data << " "; 
      } 
    }
    ```

### BFS

-   Level Order Traversal이진 탐색 트리(Binary Search Tree)
    
    ```cpp
    void LevelOrder(TreeNode *root) { 
        if (root == nullptr) return; 
        queue<TreeNode*> q; 
        q.push(root); 
   	    while (!q.empty()) { 
       	    TreeNode* node = q.front(); q.pop(); 
       	    cout << node->data << " "; 
       	    if (node->leftChild != nullptr) q.push(node->leftChild); 
       	    if (node->rightChilde != nullptr) q.push(node->rightChild); 
   	    }
    }
    ```

## 이진 탐색 트리

### 이진 탐색 트리의 성질
-   왼쪽 자식은 부모보다 작음
-   오른쪽 자식은 부모보다 큼
-   어떤 두 노드도 동일한 키를 갖지 않음

### 이진 탐색 트리의 탐색
- key 찾기   

    ```cpp
    TreeNode* SearchBST(TreeNode *node, int key) {
        if (node == nullptr) return 0;
        if (key < node->data) return SearchBST(node->leftChild);
        if (key > node->data) return SearchBST(node->rightChild);
        return node;
    }
    ```

### 이진 탐색 트리의 삽입
-   key 삽입

    ```cpp
    bool Insert(TreeNode *root, int key) {
        TreeNode *p = root;
        TreeNode *q = nullptr;

        while (p != nullptr) {
            q = p;
            if (key == p->data) return false;
            if (key < p->data) p = p->leftChild;
            else if (key > p->data) p = p->rightChild;
        }
        // q의 자식 중 하나에 삽입해야 함
        TreeNode *t = new TreeNode(key);
        if (root == nullptr) root = t;
        else if (key < q->data) q->leftChild = t;
        else q->rightChild = t;

        return true;
    }
    ```

### 이진 탐색 트리의 삭제
-   자식이 없으면, 단순 삭제
-   자식이 하나라면, 삭제된 노드의 위치에 자식 노드 이동
-   자식이 둘이라면, 왼쪽 서브트리에서 가장 큰 원소로 대체하거나 오른쪽 서브트리에서 가장 작은 원소로 대체

## 힙(Heap)

-   우선순위 큐를 구현하기 위한 완전 이진 트리 기반의 자료구조

### 최대 힙(Max Heap)
-   각 노드의 키 값이 자식 노드의 키 값보다 작지 않은 완전 이진 트리

### 최소 힙(Min Heap)
-   각 노드의 키 값이 자식 노드의 키 값보다 크지 않은 완전 이진 트리

### 힙의 삽입과 삭제(최대 힙 기준)
-   삽입
    ```cpp
    void HeapPush(int num) {
        int currentNode = ++heapSize;
        while (currentNode != 1 and heap[currentNode/2] < num) {
            heap[currentNode] = heap[currentNode/2];
            currentNode /= 2;
        }
        
        heap[currentNode] = num;
    }
    ```
-   삭제
    ```cpp
    void HeapPop() {
        int lastE = heap[heapSize--];
        int currentNode = 1;
        int child = 2;

        while (child <= heapSize) {
            if (child < heapSize and heap[child] < heap[child + 1])
                child++;
            if (lastE >= heap[child]) // currentNode에 lastE를 삽입 가능한가?
                break;
            heap[currentNode] = heap[child];
            currentNode = child;
            child *= 2;
        }
        
        heap[currentNode] = lastE;
    }
    ```
