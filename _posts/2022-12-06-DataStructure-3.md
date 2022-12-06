---
title: "링크드 리스트"
excerpt: "싱글리/더블리 링크드 리스트"

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

date: 2022-12-06
last_modified_at: 2022-12-06
---
# 링크드 리스트
링크드 리스트는 데이터를 순서대로 저장하고 요소를 계속해서 추가할 수 있다.  

노드라는 단위의 데이터를 저장하고 데이터가 저장된 노드들을 순서대로 연결시켜 만든 자료구조이다.  

각 노드는 하나의 객체로 표현된다. 각 노드객체는 data와 next속성을 가지고 있다. data에 넣고싶은 값을 넣고 next는 다음 속성에 대한 레퍼런스이다. n1노드객체와 n2노드객체가 있을 때 n1과 n2를 연결 시키려면 n1.next = n2를 하면 된다. 즉, n1.next는 n2에 대한 레퍼런스이다. 여기서 링크드 리스트의 시작점인 첫 번째 노드를 head 노드라고 한다. 

링크드 리스트의 접근 시간 복잡도는 인덱스 x에 있는 노드에 접근하려면 head에서 다음 노드로 x번 가면 된다. 그래서 O(n)이다.  

```python
class Node:
    """
    링크드 리스트의 노드 클래스
    """
    def __init__(self, data):
        self.data = data  # 노드가 저장하는 데이터
        self.next = None  # 다음 노드에 대한 레퍼런스


class LinkedList:
    """링크드 리스트 클래스"""
    def __init__(self):
        self.head = None  # 링크드 리스트의 가장 앞 노드
        self.tail = None  # 링크드 리스트의 가장 뒤 노드

    def delete_after(self, previous_node):
        """링크드 리스트 삭제연산. 주어진 노드 뒤 노드를 삭제한다"""
        data = previous_node.next.data

        # 지우려는 노드가 tail 노드일 때
        if previous_node.next is self.tail:
            previous_node.next = None
            self.tail = previous_node
        # 두 노드 사이 노드를 지울 때
        else:
            previous_node.next = previous_node.next.next

        # 링크드 리스트에서 노드를 삭제할 때는 지워지는 노드의 데이터를 리턴하는 것이 관습이다
        return data

    def pop_left(self):
        """링크드 리스트의 가장 앞 노드 삭제 메소드. 단, 링크드 리스트에 항상 노드가 있다고 가정한다"""
        data = self.head.data

        # 삭제 하려는 데이터가 링크드 리스트의 마지막 남은 데이터일 때
        if self.head is self.tail:
            self.head = None
            self.tail = None
        else:
            self.head = self.head.next

        return data

    def insert_after(self, previous_node, data):
        """링크드 리스트 주어진 노드 뒤 삽입 연산 메소드"""
        new_node = Node(data)

        # 가장 마지막 순서 삽입
        if previous_node is self.tail:
            self.tail.next = new_node
            self.tail = new_node
        else:  # 두 노드 사이에 삽입
            new_node.next = previous_node.next
            previous_node.next = new_node

    def prepend(self, data):
        """링크드 리스트의 가장 앞에 데이터 삽입"""
        new_node = Node(data)

        if self.head is None:
            self.head = new_node
            self.tail = new_node
        else:
            new_node.next = self.head
            self.head = new_node

    def find_node_at(self, index):
        """링크드 리스트 접근 연산 메소드. 파라미터 인덱스는 항상 있다고 가정"""
        iterator = self.head

        for _ in range(index):
            iterator = iterator.next

        return iterator

    def find_node_with_data(self, data):
        """링크드 리스트에서 탐색 연산 메소드. 단, 해당 노드가 없으면 None을 리턴한다"""
        iterator = self.head

        while iterator is not None:
            if iterator.data == data:
                return iterator
            iterator = iterator.next

        return None

    def append(self, data):
        """링크드 리스트 추가 연산 메소드"""
        new_node = Node(data)

        if self.head is None:  # 링크드 리스트가 비어 있는 경우
            # 새로운 노드가 링크드 리스트의 처음이자 마지막 노드가 된다
            self.head = new_node
            self.tail = new_node
        else:  # 링크드 리스트가 비어 있지 않은 경우
            self.tail.next = new_node  # 가장 마지막 노드 뒤에 새로운 노드 추가
            self.tail = new_node  # 마지막 노드를 추가한 노드로 변경

    def __str__(self):
        """링크드 리스트를 문자열로 표현해서 리턴하는 메소드"""
        res_str = "|"

        iterator = self.head

        # 링크드 리스트를 끝까지 돈다
        while iterator is not None:
            res_str += f" {iterator.data} |"
            iterator = iterator.next  # 다음 노드로 넘어간다

        return res_str
```

## 노드와 링크드 리스트
```python
class Node:
    """
    링크드 리스트의 노드 클래스
    """
    def __init__(self, data):
        self.data = data  # 노드가 저장하는 데이터
        self.next = None  # 다음 노드에 대한 레퍼런스


class LinkedList:
    """링크드 리스트 클래스"""
    def __init__(self):
        self.head = None  # 링크드 리스트의 가장 앞 노드
        self.tail = None  # 링크드 리스트의 가장 뒤 노드
```
이렇게 노드를 만들 수 있다. data와 next속성을 가지며 next에 다음 노드객체를 담아 연결한다. head노드와 tail노드는 객체를 만들 때 자동으로 생성되게 해서 항상 존재한다.  

## 추가
```python
def append(self, data):
    """링크드 리스트 추가 연산 메소드"""
    new_node = Node(data)

    if self.head is None:  # 링크드 리스트가 비어 있는 경우
        # 새로운 노드가 링크드 리스트의 처음이자 마지막 노드가 된다
        self.head = new_node
        self.tail = new_node
    else:  # 링크드 리스트가 비어 있지 않은 경우
        self.tail.next = new_node  # 가장 마지막 노드 뒤에 새로운 노드 추가
        self.tail = new_node  # 마지막 노드를 추가한 노드로 변경
```
append함수는 링크드 리스트에 노드를 추가하기 위한 함수다. 링크드 리스트가 비었을 경우에는 추가되는 노드가 처음이자 마지막이므로 head이면서 tail로 지정한다.  

비어있지 않을 경우에는 가장 마지막 노드의 next가 새로운 노드를 가리키게 하고 tail을 새로운 노드로 변경한다.  

## 접근
```python
    def find_node_at(self, index):
    """링크드 리스트 접근 연산 메소드. 파라미터 인덱스는 항상 있다고 가정"""
    iterator = self.head

    for _ in range(index):
        iterator = iterator.next

    return iterator
```
해당 인덱스로 접근하려면 인덱스만큼 next로의 접근을 반복하면 된다.  

## 탐색
```python
def find_node_with_data(self, data):
    """링크드 리스트에서 탐색 연산 메소드. 단, 해당 노드가 없으면 None을 리턴한다"""
    iterator = self.head

    while iterator is not None:
        if iterator.data == data:
            return iterator
        iterator = iterator.next

    return None
```
링크드 리스트를 처음부터 찾는 값이 나올 때 까지 돌린다. 링크드 리스트의 마지막인 tail은 next가 None이므로 None이 아닐 때 까지만 돌린다.  

## 삽입
```python
def insert_after(self, previous_node, data):
    """링크드 리스트 주어진 노드 뒤 삽입 연산 메소드"""
    new_node = Node(data)

    # 가장 마지막 순서 삽입
    if previous_node is self.tail:
        self.tail.next = new_node
        self.tail = new_node
    else:  # 두 노드 사이에 삽입
        new_node.next = previous_node.next
        previous_node.next = new_node
```
주어진 노드 뒤에 삽입한다. 가장 마지막 순서에 삽입할 때는 추가와 똑같다.  

두 노드 사이에 삽입할 때는 A와 B사이에 삽입한다고 하면 새로운 노드의 next가 B를 가리키게 한다. 그리고 A의 next가 새로운 노드를 가리키게 하면 된다.  

### 가장 앞에 삽입
```python
 def prepend(self, data):
    """링크드 리스트의 가장 앞에 데이터 삽입"""
    new_node = Node(data)

    # 링크드 리스트가 비었을 때
    if self.head is None:
        self.head = new_node
        self.tail = new_node
    else:
        new_node.next = self.head
        self.head = new_node
```
가장 앞에 삽입할 때 링크드 리스트가 비었을 때는 추가와 동일하다.  

링크드 리스트가 비어있지 않을 때는 새로운 노드의 next가 head를 가리키게 하고 head를 새로운 노드로 바꾼다.  

## 삭제
```python
def delete_after(self, previous_node):
    """링크드 리스트 삭제연산. 주어진 노드 뒤 노드를 삭제한다"""
    data = previous_node.next.data

    # 지우려는 노드가 tail 노드일 때
    if previous_node.next is self.tail:
        previous_node.next = None
        self.tail = previous_node
    # 두 노드 사이 노드를 지울 때
    else:
        previous_node.next = previous_node.next.next

    # 링크드 리스트에서 노드를 삭제할 때는 지워지는 노드의 데이터를 리턴하는 것이 관습이다
    return data
```
주어진 노드 뒤 노드를 삭제할 때 지우려는 노드가 tail일 때는 주어진 노드가 아무것도 가리키게 하지 않게하고 tail을 주어진 노드로 교체한다.  

두 노드 사이 노드를 지울 때 A -> B -> C 노드 순서에서 B노드를 삭제한다고 하면 A의 next가 C를 가리키게 하면 된다.  

### 가장 앞에 삭제
```python
def pop_left(self):
    """링크드 리스트의 가장 앞 노드 삭제 메소드. 단, 링크드 리스트에 항상 노드가 있다고 가정한다"""
    data = self.head.data

    # 삭제 하려는 데이터가 링크드 리스트의 마지막 남은 데이터일 때
    if self.head is self.tail:
        self.head = None
        self.tail = None
    else:
        self.head = self.head.next

    return data
```
가장 앞 노드를 삭제할 때 삭제할 데이터가 링크드 리스트에 마지막으로 남은 데이터라면 그 노드는 head이자 tail이므로 head와 tail을 None으로 한다.  

여러개 남은 경우에는 head를 삭제할 다음 노드로 변경한다.  

## 링크드 리스트 시간 복잡도
### 접근
인덱스n의 데이터에 접근하려면 head노드부터 n번 다음 노드를 찾아가야 한다.  
시간 복잡도는 O(n)이다.  

### 탐색
선형 탐색을 하므로 O(n)이다.  

### 삽입/삭제
삽입/삭제 자체는 해당 인덱스의 주변 노드들에 연결된 레퍼런스만 수정하므로 O(1)이지만 결국 삽입/삭제를 하기 위해선 접근을 해야하므로 O(n)이다. 다만 가장 앞의 노드를 삽입/삭제는 O(1), 가장 뒤의 노드를 삽입은 O(1)이다. 가장 뒤의 노드를 삭제는 바로 앞 노드가 필요하므로 O(n)만큼 걸린다.  

# 더블리 링크드 리스트
각 노드가 바로 다음 노드에 대한 레퍼런스만 갖는 경우를 싱글리 링크드 리스트라고 한다.  
각 노드가 바로 다음 노드와 바로 전 노드의 레퍼런스를 함께 갖는 경우를 더블리 링크드 리스트라고 한다.  

접근, 탐색은 싱글리 링크드 리스트와 동일하다.  

## 노드와 링크드 리스트
```python
class Node:
    """링크드 리스트의 노드 클래스"""
    def __init__(self, data):
        self.data = data  # 노드가 저장하는 데이터
        self.next = None  # 다음 노드에 대한 레퍼런스
        self.prev = None  # 전 노드에 대한 레퍼런스


class LinkedList:
    """링크드 리스트 클래스"""
    def __init__(self):
        self.head = None  # 링크드 리스트의 가장 앞 노드
        self.tail = None  # 링크드 리스트의 가장 뒤 노드
```
더블리 리스트에는 전 노드에 대한 레퍼런스가 하나 추가된다.  

## 추가
```python
    def append(self, data):
        """링크드 리스트 추가 연산 메소드"""
        new_node = Node(data)  # 새로운 데이터를 저장하는 노드

        # 링크드 리스트가 비어 있는 경우
        if self.head is None:
            self.head = new_node
            self.tail = new_node
        else:  # 링크드 리스트에 데이터가 이미 있는 경우
            self.tail.next = new_node
            new_node.prev = self.tail
            self.tail = new_node
```
링크드 리스트가 비었을 떄의 경우는 싱글리 리스트와 동일하고  

링크드 리스트에 데이터가 이미 존재하는 경우에는 tail이 새로운 노드를 가리키게 하고 새로운 노드의 prev가 tail을 가리키게 한다. 그리고 tail을 새로운 노드로 교체한다.  

## 삽입
```python
    def insert_after(self, previous_node, data):
        """링크드 리스트 추가 연산 메소드"""
        new_node = Node(data)

        # 마지막 노드 뒤에 삽입할 때
        if previous_node is self.tail:
            self.tail.next = new_node  # 새 노드를 tail노드의 다음으로 지정
            new_node.prev = self.tail  # tail노드를 새 노드의 전 노드로 지정
            self.tail = new_node  # 새 노드를 tail노드로 지정
        # 두 노드 사이에 삽입할 때
        else:
            # 새 노드를 기존의 링크드 리스트에 연결
            new_node.prev = previous_node
            new_node.next = previous_node.next

            # 기존의 노드들의 앞과 다음 레퍼런스를 새롭게 생성한 노드로 지정
            previous_node.next.prev = new_node
            previous_node.next = new_node
```
주어진 노드 뒤에 삽입한다.  

마지막 노드 뒤에 삽입할 때는 tail의 next가 새로운 노드를 가리키게 하고 새 노드의 prev가 tail을 가리키게 한 다음 tail을 새 노드로 교체한다.  

두 노드 사이에 삽입할 때 A와 B사이에 삽입한다고 하면 새 노드의 prev가 A를 가리키게 하고 next가 B를 가리키게 한다. 그리고 B의 prev가 새 노드를 가리키게 하고 A의 next가 새 노드를 가리키게 한다.  

### 가장 앞 삽입
```python
    def prepend(self, data):
        """링크드 리스트 가장 앞에 데이터를 추가시켜주는 메소드"""
        new_node = Node(data)

        # 링크드 리스트가 비었을 때
        if self.head is None:
            self.head = new_node
            self.tail = new_node
        # 링크드 리스트가 안 비었을 때
        else:
            new_node.next = self.head
            self.head.prev = new_node
            self.head = new_node
```
가장 앞에 삽입할 때 링크드 리스트가 비었으면 싱글리 리스트와 동일하고  

링크드 리스트가 비어있지 않을 때는 새 노드의 next가 head를 가리키게 하고 head의 prev가 새 노드를 가리키게 한다. 그리고 head를 새 노드로 교체한다.  

## 삭제
```python
    def delete(self, node_to_delete):
        """더블리 링크드 리스트 삭제 연산 메소드"""
        # 마지막 남은 데이터를 삭제할 때
        if node_to_delete is self.head and node_to_delete is self.tail:
            self.head = None
            self.tail = None
        
        # 가장 앞 데이터 삭제할 때
        elif node_to_delete is self.head:
            self.head = self.head.next
            self.head.prev = None
            
        # 가장 뒤 데이터 삭제할 때
        elif node_to_delete is self.tail:
            self.tail = self.tail.prev
            self.tail.next = None
            
        # 두 노드 사이의 데이터 삭제할 때
        else:
            node_to_delete.prev.next = node_to_delete.next
            node_to_delete.next.prev = node_to_delete.prev
        
        # 삭제하는 노드 데이터 리턴
        return node_to_delete.data
```
삭제할 때는 4가지 경우가 있다. 마지막 남은 데이터를 삭제할 때는 head와 tail을 None으로 만들면 된다.  

가장 앞 데이터를 삭제할 때는 head다음의 노드를 head로 지정하고 prev를 None으로 한다.  

가장 뒤 데이터를 삭제할 때는 tail이전의 노드를 tail로 지정하고 next를 None으로 한다.  

두 노드 사이의 데이터를 삭제할 때 A, B, C노드가 순서대로 있을 때 B노드를 삭제하려면 A의 next가 C를 가리키게하고 C의 prev가 A를 가리키게 하면 된다.  


## 더블리 리스트 시간 복잡도
시간 복잡도는 하나만 빼고 모두 동일하다.  
가장 뒤에 접근해서 삭제할 때는 O(1)만큼 걸린다.  
싱글리 링크드 리스트에서는 tail전 노드에 접근을해 파라미터를 넘겨줘야 했기 때문에 O(n)만큼 걸렸지만 더블리 링크드 리스트에서는 지우려는 노드 자체를 파라미터로 받기 때문에 tail노드로 바로 접근해 O(1)이다.  

# 싱글리/더블리 링크드 리스트
싱글리 링크드 리스트는 특정 노드에서 앞에 있는 노드들에 접근할 수 없다. 더블리 링크드 리스트는 어떤 노드던지 링크드 리스트 안 모든 노드에 접근할 수 있다.  

실제 데이터를 제외한 나머지 데이터들 즉, 레퍼런스를 저장할 공간을 추가적 공간이라 고 했을 때 싱글리 링크드 리스트는 실제 데이터와 다음 노드에 대한 레퍼런스를 저장하니 추가적 공간은 O(n - 1)이므로 O(n)이다. 더블리 링크드 리스트는 실제 데이터와 다음/이전 노드에 대한 레퍼런스를 저장하니 추가적 공간은 O(2n - 2)이므로 O(n)이다. 추가적 공간의 공간 복잡도는 동일하지만 실제로는 2배정도의 차이가 난다.  


 




