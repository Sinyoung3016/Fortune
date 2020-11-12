---
layout: post
title: "[알고리즘] Search"
date: 2020-11-12 00:00:00
categories: [SOPHOMORE]
tags: [ALGORITHM]
last_modified_at: 2020-11-12
---

### Sequential Search

<p>
: 데이터의 첫 부분부터 순서대로 탐색키와 데이터를 비교하여 원하는 데이터를 찾는 방법.
</p>

<p>
* 시간 복잡도 : O(n)
</p>

```{.cpp}
int sequentialSearch(int[] data, int key){
    for(int i = 0; i < data.size(); i++)
        if(data[i] == key) return i;
    return -1;
}
```

---

### Binary Search

<p>
: 데이터의 가운데에 있는 항목을 키값과 비교하여 다음 탐색 위치를 결정하고,
키를 찾을 때까지 이진 탐색을 반복적으로 수행하여 원하는 데이터를 찾는 방법.
</p>

<p>
* 이미 정렬이 되어있다는 것을 전제로함.
<br>* 찾는 키값 > 원소의 키(n/2)값, (n/2 + 1)부터 n번째 데이터에 대해서 탐색.
<br>* 찾는 키값 < 원소의 키(n/2)값, 1부터 (n/2)번째 데이터에 대해서 탐색.
</p>

<p>
* 시간 복잡도 : O(logN)
</p>

```{.cpp}
int binarySearch(int[] data, int key){
   int left = 0, right = data.size()-1, mid;
    while(left <= right){
        mid = (left + right) / 2;
        if(key > data[mid]) left = mid + 1
        else id (key < data[mid]) right = mid - 1;
        else return mid;
    }
}
```

<br>
<br>



