---
title: 선택 정렬(Selection Sort)
date: 2025-01-30 20:20:00 +09:00
categories: [Study, Algorithms]
tags:
  [
    선택 정렬,
    selection sort,
  ]
---

#   선택 정렬(Selection Sort)

##  선택 정렬이란? 
-   n 번째 자리에 n 번째로 작은 수를 선택해서 넣는 알고리즘
-   1회전을 수행하고 나면 가장 작은 원소가 맨 앞으로 이동

##  장점
-   구현이 간단함
-   원소의 이동 횟수가 미리 결정됨
-   제자리 정렬

##  단점
-   불안정 정렬

##  시간복잡도
-   최선, 평균, 최악의 경우 모두 O(n^2)임

##  코드 
```cpp
//  오름차순으로 정렬
void selection_sort(int a[], int n) {
    int i, j, min_idx;
    for (i = 0; i < n - 1; i++) {
        min_idx = i;
        for (j = i + 1; j < n; j++)
            if (a[j] < a[min_idx])
                min_idx = j;
        swap(a[i], a[min_idx]);
    }
}
```