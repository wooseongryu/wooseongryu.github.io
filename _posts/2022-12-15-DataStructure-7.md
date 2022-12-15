---
title: "힙"
excerpt: "힙, 힙 정렬, 우선순위 큐"

categories:
    - 자료구조
tags:
    - [자료구조]

toc: true
toc_sticky: true

comments:
  provider: "utterances"
  utterances:
    theme: "github-light" # "github-dark"
    issue_term: "pathname"
    label: "comment" # Optional - must be existing label.

date: 2022-12-15
last_modified_at: 2022-12-15
---
# 힙
힙은 두개의 조건을 만족하는 트리다. 첫번째 조건은 형태 속성이며 힙은 완전 이진 트리여야 한다는 조건이다. 두번째 조건은 힙 속성이며 모든 노드의 데이터는 자식 노드들의 데이터보다 크거나 같다는 조건이다.  

# 정렬
데이터를 재배치하는 구체적인 방법을 정렬 알고리즘이라 한다. 삽입 정렬, 선택 정렬, 퀵 정렬, 합병 정렬 등이 있다. 힙 자료구조를 사용해 데이터를 정렬하는 알고리즘을 힙 정렬이라 한다.  

# 힙 구현
힙은 완전 이진 트리이므로 동적 배열로 구현한다. 만약 힙 속성을 만족하지 않는다면 만족하도록 정렬시켜 줘야 한다. 이 과정을 heapify라고 한다. heapify는 파라미터로 노드 하나를 받는다. 이 노드를 부모노드라 하면 부모노드와 양쪽의 자식 중 가장 큰 것을 골라 이것이 부모노드가 아니라면 서로 바꾼다. 부모노드가 가장 크다면 아무것도 하지 않는다. 시간 복잡도는 트리에 저장된 노드 수를 n이라 했을 때 최악의 경우는 파라미터로 root노드를 넘겼을 때 leaf노드까지 내려가는 경우고 O(lg(n))이다.  

```python
def swap(tree, index_1, index_2):
    """완전 이진 트리의 노드 index_1과 노드 index_2의 위치를 바꿔준다"""
    temp = tree[index_1]
    tree[index_1] = tree[index_2]
    tree[index_2] = temp


def heapify(tree, index, tree_size):
    """heapify 함수"""

    # 왼쪽 자식 노드의 인덱스와 오른쪽 자식 노드의 인덱스를 계산
    left_child_index = 2 * index
    right_child_index = 2 * index + 1

    largest = index

    if 0 < left_child_index < tree_size and tree[largest] < tree[left_child_index]:
        largest = left_child_index

    elif 0 < right_child_index < tree_size and tree[largest] < tree[right_child_index]:
        largest = right_child_index

    if largest != index:
        swap(tree, index, largest)
        heapify(tree, largest, tree_size)
```

완전 이진 트리가 리스트로 구현되어 있을 때 뒤에서 부터 앞으로 heapify를 호출하면 특정 노드 아래의 부분 트리가 힙 속성을 가지게 된다. n개의 노드가 있을 때 특정 노드의 heapify를 호출하는 것은 O(lg(n))이 걸린다. 힙을 만들려면 heapify를 n개의 노드에 모두 호출해야 하므로 O(nlg(n))만큼 걸린다.  

# 힙 정렬
힙을 만든다  
root노드와 마지막 노드를 바꾼다  
바꾼 노드는 없는 노드 취급한다  
새로운 root노드가 힙 속성을 지킬 수 있게 root노드에 heapify를 호출한다  
모든 인덱스를 돌 때 까지 반복한다  

```python
def swap(tree, index_1, index_2):
    ...


def heapify(tree, index, tree_size):
    ...


def heapsort(tree):
    """힙 정렬 함수"""
    tree_size = len(tree)

    for i in range(tree_size - 1, 0, -1):
        heapify(tree, i, tree_size)

    for i in range(tree_size - 1, 0, -1):
        swap(tree, 1, i)
        heapify(tree, 1, i)
```

내림 차순으로 정렬하려면 힙 속성을 부모 노드의 데이터가 자식 노드의 데이터보다 작아야 한다로 반대로 바꾸고 똑같은 알고리즘을 적용하면 된다.  

## 힙 정렬 시간 복잡도
1. 힙을 만드는데 O(nlg(n))  
2. root노드와 마지막 노드를 바꾸는데 O(1)  
3. 새로운 root노드에 heapify는 O(lg(n))  
2와 3의 과정을 반복하면 O(nlg(n)), 전체 과정은 O(2nlg(n)), 그래서 결과적으로 O(nlg(n))이 걸린다.  

선택 정렬 - O(n^2)  
삽입 정렬 - O(n^2)  
합병 정렬 - O(nlg(n))  
퀵 정렬 - 평균 O(nlg(n)), 최악O(n^2)  
힙 정렬 - O(nlg(n))  

# 우선순위 큐
힙은 보통 2가지 목적으로 사용되는데 정렬과 추상 자료형인 우선순위 큐를 구현하기 위함이다. 우선순위 큐는 데이터를 저장할 수 있고 각 데이터에 우선순위가 있다. 저장한 데이터가 우선순위 순서대로 나온다.  

## 힙으로 우선순위 큐 구현
### 삽입
힙에 데이터를 삽입하려면  
1. 힙의 마지막 인덱스에 데이터를 삽입한다.  
2. 삽입한 데이터와 부모 노드의 데이터를 비교한다.  
3. 부모 노드의 데이터가 더 작으면 둘의 위치를 바꿔준다.  
새로 삽입한 노드가 제 위치를 찾을 때 까지 2와 3을 반복한다.  

```python
def swap(tree, index_1, index_2):
    ...


def reverse_heapify(tree, index):
    """삽입된 노드를 힙 속성을 지키는 위치로 이동시키는 함수"""
    parent_index = index // 2  # 삽입된 노드의 부모 노드의 인덱스 계산

    if 0 < parent_index < len(tree) and tree[parent_index] < tree[index]:
        swap(tree, parent_index, index)
        reverse_heapify(tree, parent_index)


class PriorityQueue:
    """힙으로 구현한 우선순위 큐"""
    def __init__(self):
        self.heap = [None]  # 파이썬 리스트로 구현한 힙

    def insert(self, data):
        """삽입 메소드"""
        self.heap.append(data)
        reverse_heapify(self.heap, len(self.heap) - 1)

    def __str__(self):
        return str(self.heap)
```

시간 복잡도는 1, 2, 3단계 모두 O(1)이고 최악의 경우 2단계를 힙의 높이만큼 반복하니 O(lg(n))이다. 결국 시간 복잡도는 O(lg(n))이다.  

### 추출
가장 큰 데이터를 우선순위로 할 때 힙 속성을 만족한다면 root노드가 가장 크므로 root노드를 추출한다. 힙에서 root노드 데이터를 추출하려면  
1. root노드와 마지막 노드를 바꾼다.  
2. 마지막 노드의 데이터를 변수에 저장하고 마지막 노드를 삭제한다.  
3. 새로운 root노드에 heapify를 호출해서 망가진 힙 속성을 고친다.  
4. 변수에 저장된 데이터를 리턴한다.  

```python
def swap(tree, index_1, index_2):
    ...


def heapify(tree, index, tree_size):
    ...


def reverse_heapify(tree, index):
    ...


class PriorityQueue:
    """힙으로 구현한 우선순위 큐"""
    def __init__(self):
        self.heap = [None]  # 파이썬 리스트로 구현한 힙

    def insert(self, data):
        """삽입 메소드"""
        self.heap.append(data)  # 힙의 마지막에 데이터 추가
        reverse_heapify(self.heap, len(self.heap)-1)  # 삽입된 노드(추가된 데이터)의 위치를 재배치

    def extract_max(self):
        """최우선순위 데이터 추출 메소드"""
        swap(self.heap, 1, len(self.heap) - 1)
        tmp = self.heap.pop()
        heapify(self.heap, 1, len(self.heap))

        return tmp

    def __str__(self):
        return str(self.heap)
```

시간 복잡도는 1, 2, 4단계는 O(1), 3단계는 O(lg(n))이므로 시간 복잡도는 O(lg(n))이다.  

## 정렬된 동적 배열로 우선순위 큐 구현
동적 배열에 데이터가 정렬된 채로 있을 때 삽입을 하려면 새로운 데이터가 어느 위치에 들어가야 하는지 찾아야 하고 이진 탐색을 사용하면 O(lg(n))이 걸린다. 그리고 그 위치에 데이터를 삽입하는 것은 최악의 경우 O(n)이 걸린다. 그러므로 삽입은 O(n)이 걸린다.  
추출을 하려면 동적 배열이 정렬된 상태라면 우선순위가 가장 높은 데이터는 배열의 끝에 있을 것이므로 O(1)이 걸린다.  

## 정렬된 더블리 링크드 리스트로 우선순위 큐 구현
삽입을 하려면 삽입할 위치를 찾아야 하고 링크드 리스트에선 선형 탐색을 해야한다. 이 때 최악의 경우 O(n)이 걸린다. 위치만 정해지면 링크드 리스트에서 데이터를 삽입하는 것은 O(1)이 걸린다. 그러므로 삽입은 O(n)이 걸린다.  
추출은 더블리 링크드 리스트에서 마지막 데이터를 추출하는 데는 O(1)이 걸린다.  

||데이터 삽입|데이터 추출|
|:-:|
|정렬된 동적 배열|O(n)|O(1)|
|정렬된 더블리 링크드 리스트|O(n)|O(1)|
|힙|O(lg(n))|O(lg(n))|

우선순위 큐는 새로운 데이터를 삽입할 일이 많으면 힙으로 구현하고 기존 데이터를 추출할 일이 많으면 동적 배열이나 더블리 링크드 리스트로 구현하면 된다.  

