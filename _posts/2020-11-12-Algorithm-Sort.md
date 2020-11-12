---
layout: post
title: "[알고리즘] Sort"
date: 2020-11-12 00:00:00
categories: [SOPHOMORE]
tags: [ALGORITHM]
last_modified_at: 2020-11-12
---

### Insertion Sort

<p>
: 모든 데이터를 앞에서부터 차례로 이미 정렬돤 부분과 비교하여, 자신의 위치를 찾아 삽입하는 알고리즘.
</p>

```{.java}
    boolean sort(E[] aList){
      if(aList.length <= 1) return false;

      int minLoc = 0;
      for(int i = 1; i < aList.length; i++)
          if(this.compare(aList[minLoc], aList[i]) > 0) minLoc =i;
          this.swap(aList,minLoc,0);

          for(int i = 2;i < aList.length; i++){
              E insertedElement = aList[i];
              int j = i-1;
              while(this.compare(aList[j], insertedElement) > 0){
                  aList[j+1] = aList[j];
                  j--;
              }
              aList[j+1] = insertedElement;
            }
        return true;
    }
```

<p>
* Worst 시간 복잡도 : O(n^2)
</p>

---

### Quick Sort

<p>
: pivot을 기준으로 하여, 두개의 비균등한 크기로 분할한 후 정렬.
이를 반복하여 전체적으로 정렬된 리스트를 만듬.
</p>

<p>
1. 피봇을 기준으로 피봇보다 작은 값은 왼쪽에, 큰 값은 오른쪽으로 swap.
<br>2. 피봇을 기준으로 두개의 리스트로 분할한 후, 위의 과정을 반복함.
<br>3. 리스트의 크기가 0이나 1이 될때까지 반복.
</p>

<p>
* Worst 시간 복잡도 : O(n^2)
<br>평균적으로는 O(NlogN)으로 같은 시간복잡도를 가지는 다른 알고리즘과 비교할 때, 가장 빠름.
추가적인 메모리도 필요로 하지 않음.
* 정렬되어있는 경우에 수행시간이 더 걸림. 따라서 pivot은 중간값으로 설정하는 것이 좋음.
</p>


```{.java}
    void quickSort(int[] aList, int left, int right) {
      if(left<right){
        int pivot = this.pivot(aList,left,right);
        this.swap(aList,left,pivot);
        E pivotElement = aList[left];
        int toRight = left;
        int toLeft = right+1;

        do{
            do{ toRight++;} while(this.compare(aList[toRight],pivotElement)<0);
            do{ toLeft--;} while(this.compare(aList[toLeft],pivotElement)>0);

            if(toRight<toLeft)
              this.swap(aList,toRight,toLeft);
          }while (toRight < toLeft);

        this.swap(aList,left,toLeft);

        quickSort(aList, left, toLeft - 1);
        quickSort(aList, toLeft + 1, right);
    }
}
```

---

### Heap Sort

<p>
: 최대 힙 또는 최소 힙을 만들어 정렬.
</p>

<p>
1. 정렬해야 할 n개의 요소를 최대 힙(내림차순)을 만듬.
<br>2. 힙에서 요소를 하나씩 꺼내 배열의 뒤부터 저장.
<br>3. 최대 값부터 삭제되므로 내림차순 정렬.
</p>

<p>
* Heap은 완전이진트리이며, 1차원 배열로 구현.
<br>* 정렬을 위해 루트 값을 삭제하고, 해당 자리에 마지막 노드의 값을 가져오고 다시 힙을 재구성.
</p>

<p>
* Worst 시간 복잡도 : O(NlogN)
<br>* 내림차순 정렬은 최대 힙, 오름차순 정렬은 최소 힙을 구성.
<br>* 전체 정렬이 아니고, 가장 큰 값이 몇개만 필요할때 사용하기 좋음.
</p>


```{.java}
    private void adjust(E[] aList,int root, int endOfHeap){
        int parent = root;
        E rootElement = aList[root];
        while((parent*2) <= endOfHeap){
            int biggerChild = parent*2;
            int rightChild = biggerChild+1;
            if((rightChild <= endOfHeap)&&(this.compare(aList[biggerChild], aList[rightChild]) < 0))
                biggerChild = rightChild;
            if(this.compare(rootElement, aList[biggerChild]) >= 0) break;
            aList[parent] = aList[biggerChild];
            parent = biggerChild;
        }
        aList[parent] = rootElement;
    }

    private void makeInitHeap(E[] aList){
        for(int rootOfSubtree = (aList.length-1)/2; rootOfSubtree >= 1; rootOfSubtree--){
            this.adjust(aList, rootOfSubtree, aList.length-1);
        }
    }

    private E removeMax(E[] aList, int heapSize){
        E removedElement = aList[HeapSort.HEAP_ROOT];
        aList[HeapSort.HEAP_ROOT] = aList[heapSize];
        this.adjust(aList, HeapSort.HEAP_ROOT, heapSize-1);
        return removedElement;
    }

    @Override
    public boolean sort(E[] aList){
        if(aList.length <= 1) return false;

        int minLoc = 0;
        for(int i = 1; i < aList.length; i++)
            if(this.compare(aList[minLoc], aList[i]) > 0) minLoc = i;

        this.swap(aList,minLoc,0);

        this.makeInitHeap(aList);
        for(int heapSize = aList.length-1; heapSize > 1; heapSize--){
            E maxElement = this.removeMax(aList, heapSize);
            aList[heapSize] = maxElement;
        }
        return true;
    }
```


<br>
<br>



