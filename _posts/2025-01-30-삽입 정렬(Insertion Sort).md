---
title: 삽입 정렬(Insertion Sort)
date: 2025-01-30 20:00:00 +09:00
categories: [Study, Algorithms]
tags:
  [
    삽입 정렬,
    insertion sort,
  ]
---

#   삽입 정렬(Insertion Sort)

##  삽입 정렬이란? 
-   기존의 정렬된 배열에서 올바른 위치를 찾아 새로운 원소를 삽입하는 방법

##  장점
-   대부분의 원소가 이미 정렬되어 있는 경우에 매우 효율적임
-   원소의 수가 적을 경우 간단한 알고리즘이여서 다른 복잡한 알고리즘보다 유리함
-   안정 정렬이며 제자리 정렬

##  단점
-   비교적 많은 원소의 이동이 필요

##  시간복잡도
-   최선의 경우 O(n), 평균, 최악의 경우 O(n^2)임

##  코드 
```cpp
//  오름차순으로 정렬
void insertion_sort(int a[], int n) {
    int i, j, key;
    for (i = 1; i < n; i++) {
        key = a[i];
        for (j = i - 1; j >= 0 and a[j] > key; j--)
            a[j + 1] = a[j];
        a[j + 1] = key;
    }
}
```