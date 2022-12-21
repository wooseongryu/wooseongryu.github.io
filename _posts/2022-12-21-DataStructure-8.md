---
title: "이진 탐색 트리"
excerpt: "이진 탐색 트리"

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

date: 2022-12-21
last_modified_at: 2022-12-21
---
# 이진 탐색 트리
딕셔너리나 세트를 구현하는데 쓸 수 있다. 이진 탐색 트리는 이진 트리면서 다음 속성을 지켜야 한다. 그 속성은 특정 노드를 봤을 때 왼쪽 부분 트리의 모든 노드는 그 노드의 데이터보다 작아야 하며 오른쪽 부분 트리의 모든 노드는 그 노드의 데이터보다 커야 한다. 
이진 탐색 트리를 사용하면 데이터를 쉽게 찾을 수 있고 꼭 완전 이진 트리일 필요는 없다. 

## 삽입
삽입 이후에도 이진 탐색 트리 속성이 유지돼야 한다.  

새로운 노드를 생성한다. O(1)  
root노드부터 비교하면서 저장할 위치를 찾는다. 최악의 경우 O(h + 1)
찾은 위치에 새롭게 만든 노드를 연결한다. O(1)  

시간 복잡도는 트리의 높이가 h일 때 O(1 + h + 1) 즉, O(h)이다.  

```python
    def insert(self, data):
        """이진 탐색 트리 삽입 메소드"""
        new_node = Node(data)

        # 트리가 비었으면 새로운 노드를 root 노드로 만든다
        if self.root is None:
            self.root = new_node
            return

        temp = self.root

        # 원하는 위치를 찾아간다
        while temp is not None:
            if data > temp.data:
                if temp.right_child is None:
                    new_node.parent = temp
                    temp.right_child = new_node
                    return
                else:
                    temp = temp.right_child
            else:
                if temp.left_child is None:
                    new_node.parent = temp
                    temp.left_child = new_node
                    return
                else:
                    temp = temp.left_child
```

## 탐색
특정 데이터를 갖는 노드를 리턴하는 연산이다.  

1. root노드부터 주어진 노드의 데이터와 탐색하려는 데이터를 비교한다.  
2. 탐색하려는 데이터가 더 크면 노드의 오른쪽 자식으로 간다.  
3. 탐색하려는 데이터가 더 작으면 노드의 왼쪽 자식으로 간다.  
1 ~ 3단계를 데이터를 찾을 때 까지 반복한다.  
4. 탐색하려는 노드를 찾으면 리턴한다.  

최악의 경우 트리의 높이가 h일 때 깊이가 가장 큰 데이터를 찾을 때 이고 O(h + 1)이다.  

```python
    def search(self, data):
        """이진 탐색 트리 탐색 메소드, 찾는 데이터를 갖는 노드가 없으면 None을 리턴한다"""
        tmp = self.root

        while tmp is not None:
            if data > tmp.data:
                tmp = tmp.right_child
            elif data < tmp.data:
                tmp = tmp.left_child
            else:
                return tmp

        return None
```


## 삭제
삭제하려는 데이터를 갖는 노드를 먼저 찾아야 한다. 탐색연산을 사용해 찾으면 된다. 총 3가지 경우가 있다.  

1. 삭제하려는 데이터가 leaf노드의 데이터 일 때  
부모 노드의 해당 데이터에 대한 레퍼런스를 None으로 한다. 지우려는 자식이 왼쪽인지 오른쪽인지에 따라 처리해 주면 된다.  
```python
    def delete(self, data):
        """이진 탐색 트리 삭제 메소드"""
        node_to_delete = self.search(data)  # 삭제할 노드를 가지고 온다
        parent_node = node_to_delete.parent

        # 지우려는 노드가 leaf노드일 때
        if node_to_delete.left_child is None and node_to_delete.right_child is None:
            # 지우려는 노드가 root노드일 때
            if self.root is node_to_delete:
                self.root is None
            else:
                if node_to_delete is parent_node.left_child:
                    parent_node.left_child = None
                else:
                    parent_node.right_child = None
```

2. 삭제하려는 데이터 노드가 하나의 자식 노드만 있을 때  
자식 노드가 부모 노드의 자리를 차지하면 된다.  
```python
    def delete(self, data):

    ...

        elif node_to_delete.left_child is None:  # 지우려는 노드가 오른쪽 자식만 있을 때:
            # 지우려는 노드가 root 노드일 때
            if node_to_delete is self.root:
                self.root = node_to_delete.right_child
                self.root.parent = None
            # 지우려는 노드가 부모의 왼쪽 자식일 때
            elif node_to_delete is parent_node.left_child:
                parent_node.left_child = node_to_delete.right_child
                node_to_delete.right_child.parent = parent_node
            # 지우려는 노드가 부모의 오른쪽 자식일 때
            else:
                parent_node.right_child = node_to_delete.right_child
                node_to_delete.right_child.parent = parent_node
        
        elif node_to_delete.right_child is None:  # 지우려는 노드가 왼쪽 자식만 있을 때:
            # 지우려는 노드가 root 노드일 때
            if node_to_delete is self.root:
                self.root = node_to_delete.left_child
                self.root.parent = None
            # 지우려는 노드가 부모의 왼쪽 자식일 때
            elif node_to_delete is parent_node.left_child:
                parent_node.left_child = node_to_delete.left_child
                node_to_delete.left_child.parent = parent_node
            # 지우려는 노드가 부모의 오른쪽 자식일 때
            else:
                parent_node.right_child = node_to_delete.left_child
                node_to_delete.left_child.parent = parent_node
```
삭제하려는 노드에 자식 노드가 하나만 있는 경우는 오른쪽/왼쪽 자식만 있는경우 2가지가 있다. leaf노드를 지우는 경우의 코드에서 두 자식이 없는 경우를 처리했으므로 여기서 elif를 쓰면 자식이 하나인 경우를 찾을 수 있다. 각 경우에서 지우려는 노드가 root노드일 때 지우려는 노드가 부모의 왼쪽/오른쪽 자식일 때 3가지 경우가 있다.  

3. 삭제하려는 데이터의 노드가 두 개의 자식이 있을 때  
지우려는 노드의 오른쪽 자식으로 간다.  
해당 노드의 부분트리에서 가장 작은 노드를 찾는다.  
이진 탐색 트리에서 어떤 노드보다 큰 모든 노드중 가장 작은 노드를 successor라고 한다.  
successor는 항상 leaf노드거나 오른쪽 자식만 가질 수 있다.  
삭제하려는 노드 데이터에 successor의 데이터를 저장한다.  
successor노드를 삭제한다.  
```python
    @staticmethod
    def find_min(node):
        """(부분)이진 탐색 트리의 가장 작은 노드 리턴"""
        tmp = node

        # tmp가 node를 뿌리로 갖는 부분 트리에서 가장 작은 노드일 때 까지 왼쪽 자식 노드로 간다
        while tmp.left_child:
            tmp = tmp.left_child

        return tmp

    def delete(self, data):

    ...
    
        # 지우려는 노드가 2개의 자식이 있을 때
        else:
            successor = self.find_min(node_to_delete.right_child)
            node_to_delete.data = successor.data

            # successor노드 삭제
            if successor is successor.parent.left_child:
                successor.parent.left_child = successor.right_child
            else:
                successor.parent.right_child = successor.right_child
            if successor.right_child:
                successor.right_child.parent = successor.parent
```
successor노드를 삭제할 때 크게 두 가지 경우가 있다. 삭제하려는 노드의 오른쪽 부분 트리 내에서 어떤 부모 노드의 왼쪽 자식으로 있는 경우고 이때 successor는 어떤 부모 노드의 오른쪽 자식으로 있을 수 없다. 다른 경우는 삭제하려는 노드의 바로 밑에 있는 오른쪽 자식인 경우다. 각 두 가지 상황 안에서 successor노드가 오른쪽 자식을 갖고 있거나 successor노드가 자식이 없는 상황을 생각한다. 여기서 자식이 없는 경우라면 right_child가 None일테니 successor.right_child를 successor의 부모의 새 자식으로 대입해 준다. 오른쪽 자식을 가진 경우라면 successor의 오른쪽 자식의 부모 노드로 successor의 부모로 새롭게 지정한다.  


시간 복잡도는 일단 탐색의 경우 O(h)가 걸렸고  
경우 1에선 O(1)이 걸리니 O(h)이다.  
경우 2에선 O(1)이 걸리니 O(h)이다.  
경우 3에선 successor노드를 구하는데 O(h), 지우려는 노드에 successor노드를 저장하는 데 O(h), successor노드를 지우는것은 오른쪽 자식 노드가 있으면 O(2), 없으면 O(1)이므로 O(1) 그래서 결과적으로 O(h)가 걸린다.  

## 높이
이진 탐색 트리는 완전 이진 트리가 아닌 경우가 더 많기 때문에 노드가 n개 있을 때 높이가 항상 O(lg(n))이라고 할 수 없다. 최악의 경우는 트리 안에서 노드가 직선적인 모양으로 저장됐을 때고 트리가 한쪽으로 편향됐다 또는 치우쳤다라고 표현하며 높이는 O(n)이 된다. 반대로 root노드를 기준으로 좌우가 균형을 이룰수록 트리의 높이는 작아지고 lg(n)에 가까워진다. 최악의 경우 높이가 n이 되지만 항상 그런 경우가 일어나지는 않으므로 평균을 보면 1~6의 데이터를 삽입할 때 경우의 수는 6!이다. 즉 n개의 데이터를 삽입할 때 그 순서의 경우의 수는 n!이다. 모든 순서의 확률이 동일하다고 가정할 때 평균 높이는 O(lg(n))이 된다. 그래서 평균적으로 이진 탐색 트리의 높이 h는 O(lg(n))이다 라고 할 수 있긴 하지만 삽입, 삭제 연산들을 반복하다보면 균형을 쉽게 잃게 되어 높이가 O(lg(n))일거란 보장을 할 수 없다. 그래서 이진 탐색 트리의 연산들의 시간 복잡도는 보통 높이 그대로 O(h)로 표기한다. 

## 이진 탐색 트리로 딕셔너리 구현
```python
class Node:
    """이진 탐색 트리 노드 클래스"""
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.parent = None
        self.left_child = None
        self.right_child = None
```
기존의 data를 사용해 삽입, 탐색, 삭제를 했다면 key를 사용하도록 작성한다. 연산들도 이에 맞게 수정해주면 된다. 시간 복잡도는 동일하다. 

## 이진 탐색 트리 평가
이진 탐색 트리를 사용하는 대표적인 추상 자료형은 세트와 딕셔너리가 있으며 해시 테이블로도 구현 가능하다. 삽입, 탐색, 삭제에 대한 이진 탐색 트리의 시간 복잡도는 O(h) (평균적 O(lg(n)), 최악 O(n))이며 해시 테이블의 시간 복잡도는 평균적 O(1), 최악 O(n)이다. 모든 연산에서 해시 테이블이 더 효율적인데 세트와 딕셔너리가 데이터 사이에 순서 관계를 약속하지 않는 추상 자료형이긴 하지만 순서 관계를 저장해야하는 경우가 생길 수 있는데 이진 탐색 트리는 데이터 사이에 순서를 저장하는 자료 구조이므로 이럴 때 사용하면 된다. 
