---
title: "트리"
excerpt: "트리, 이진 트리, 트리 순회"

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

date: 2022-12-12
last_modified_at: 2022-12-12
---
# 트리
트리는 데이터의 상하 관계를 저장하는 자료 구조다. 상하 관계는 계층적 관계라고도 하며 컴퓨터 폴더 구조나 클래스 상속을 통해 생기는 부모와 자식 관계들이 계층적 관계가 있는 데이터 들이다.  
여러개의 노드로 이루어져 있으며 노드들 간의 상하관계를 부모와 자식관계라 한다.  

가장 상위의 노드를 root노드라 한다.  

특정 노드의 직속 상위 노드를 부모 노드라 한다.  

특정 노드의 직속 하위 노드를 자식 노드라 한다.  

같은 부모를 갖는 노드를 형제 노드라 한다.  

자식 노드를 가지지 않는 가장 말단에 있는 노드를 leaf노드라 한다.  

특정 노드가 root노드에서 떨어져 있는 거리를 깊이라 한다. root노드는 깊이가 0이다.  

깊이 + 1을 레벨이라 한다. 레벨 1에 있는 노드들 이런식으로 특정 깊이인 노드들을 묶어서 표현할 때 사용한다.  

트리에서 가장 깊이 있는 노드의 깊이를 높이라 한다.  

현재 트리의 일부분을 이루고 있는 더 작은 트리를 부분 트리라 한다.  

# 이진 트리
각 노드가 최대 2개의 자식 노드를 갖을 수 있는 트리를 이진 트리라 한다. 

```python
class Node:
    """이진 트리 노드 클래스"""

    def __init__(self, data):
        """데이터와 두 자식 노드에 대한 레퍼런스를 갖는다"""
        self.data = data
        self.left_child = None
        self.right_child = None


# 노드 인스턴스 생성
root_node = Node(2)
node_B = Node(3)
node_C = Node(5)
node_D = Node(7)
node_E = Node(11)

# B와 C를 root노드의 자식으로 지정
root_node.left_child = node_B
root_node.right_child = node_C

# D와 E를 B의 자식으로 지정
node_B.left_child = node_D
node_B.right_child = node_E
```

## 정 이진 트리(Full Binary Tree)
모든 노드가 2개 또는 0개의 자식을 갖는 이진 트리를 말한다.  

## 완전 이진 트리(Complete Binary Tree)
이진 트리 중에서 마지막 레벨 직전은 레벨까지 모든 노드들이 다 채워진 트리를 완전 이진 트리라 한다. 마지막 레벨에서는 노드들이 다 채워질 필요는 없지만 왼쪽부터 오른쪽 방향으로는 노드들이 다 채워져야 한다.  

완전 이진 트리안에 저장된 노드가 n개일 때 높이는 항상 lg(n)에 비례한다. 완전 이진 트리의 높이는 O(lg(n))이라고 할 수 있다.  

완전 이진 트리는 아래와 같이 리스트에 저장할 수 있다.  
complete_binary_tree = [None, 1, 5, 12, 11, 9, 10, 14, 2, 10]  
1번째 인덱스부터 root노드로 시작해서 깊이가 1인 노드들을 왼쪽에서 오른쪽 방향으로 깊이가 2인 노드들을 왼쪽에서 오른쪽 방향으로..... 이렇게 반복하게해서 저장하면 된다. 자식 노드를 찾을 때는 왼쪽 자식, 오른쪽 자식을 찾는 2가지 경우가 있다. 왼쪽 자식을 찾을 때는 노드의 인덱스에 2를 곱하면 된다. 인덱스2의 자식을 찾으려면 2를 곱해 4가 되니 인덱스4가 인덱스2의 왼쪽 자식이다. 오른쪽 자식을 찾을 때는 2를 곱하고 1을 더해주면 된다. 부모 노드를 찾을 때는 2로 나누면 된다. 자식 노드의 인덱스가 홀수일 때는 2로 나누고 정수값만 가져오면 된다.  

```python
def get_parent_index(complete_binary_tree, index):
    """배열로 구현한 완전 이진 트리에서 index번째 노드의 부모 노드의 인덱스를 리턴하는 함수"""
    parent_index = index // 2
    if 0 < parent_index < len(complete_binary_tree):
        return parent_index
    return None


def get_left_child_index(complete_binary_tree, index):
    """배열로 구현한 완전 이진 트리에서 index번째 노드의 왼쪽 자식 노드의 인덱스를 리턴하는 함수"""
    left_child_index = index * 2
    if 0 < left_child_index < len(complete_binary_tree):
        return left_child_index
    return None


def get_right_child_index(complete_binary_tree, index):
    """배열로 구현한 완전 이진 트리에서 index번째 노드의 오른쪽 자식 노드의 인덱스를 리턴하는 함수"""
    right_child_index = index * 2 + 1
    if 0 < right_child_index < len(complete_binary_tree):
        return right_child_index
    return None
```

## 포화 이진 트리(Perfect Binary Tree)
모든 레벨이 빠짐없이 다 노드로 채워져있는 이진 트리를 말한다. 정 이진 트리와 완전 이진 트리의 특성을 모두 갖는다. 트리의 높이와 총 노드 수 중 하나만 알면 나머지 하나의 값을 알 수 있다.  

# 트리 순회
자료 구조에 저장된 모든 데이터를 도는 것을 순회라 한다. 재귀를 사용해 해결하려면 다음 순서대로 하면 된다.  

재귀적으로 왼쪽 부분 트리 순회  
재귀적으로 오른쪽 부분 트리 순회  
현재 노드 데이터를 출력한다  

트리는 데이터의 계층적 관계를 저장하기 때문에 데이터의 앞뒤 순서가 없지만 순회를 하게 되면 노드들 사이에 선형적 순서를 만들 수 있다.  

## pre-order
현재 노드 데이터를 출력한다  
재귀적으로 왼쪽 부분 트리 순회  
재귀적으로 오른쪽 부분 트리 순회  

root노드가 먼저 출력되고 왼쪽 부분 트리가 모두 출력되고 오른쪽 부분 트리가 모두 출력된다.  

```python
def traverse_preorder(node):
    """post-order 순회 함수"""
    if node is not None:
        print(node.data)
        traverse_preorder(node.left_child)
        traverse_preorder(node.right_child) 
```

## post-order
재귀적으로 왼쪽 부분 트리 순회  
재귀적으로 오른쪽 부분 트리 순회  
현재 노드 데이터를 출력한다  

```python
def traverse_postorder(node):
    """post-order 순회 함수"""
    if node is not None:
        traverse_postorder(node.left_child)
        traverse_postorder(node.right_child)
        print(node.data)
```

## in-order
재귀적으로 왼쪽 부분 트리 순회  
현재 노드 데이터를 출력한다  
재귀적으로 오른쪽 부분 트리 순회  

```python
def traverse_inorder(node):
    """in-order 순회 함수"""
    if node is not None:
        traverse_inorder(node.left_child)
        print(node.data)
        traverse_inorder(node.right_child)
```

