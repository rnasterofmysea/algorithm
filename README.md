# algorithm

## 1. 선형리스트(Linear List)

### 1.1 선형리스트 생성함수

```
katok = []

def add_data(friend):

    katok.append(None)
    klen = len(katok)
    katok[klen-1] = friend

add_data("다현")
add_data("정연")
add_data("쯔위")
add_data("사나")
add_data("지효")

print(katok)
```


### 1.2 데이터 삽입 함수


```
katok = ["다현", "정연", "쯔위", "사나", "지효"]

def insert_data(position, friend):
    if position < 0 or position > len(katok):
        print("데이터를 삽입할 범위를 벗어났습니다.")
        return

    katok.append(None)
    klen = len(katok)

    for i in range(klen-1, position, -1):
        katok[i] = katok[i-1]
        katok[i-1] = None
    
    katok[position] = friend

insert_data(2, '솔라')
print(katok)
insert_data(6, '문별')
print(katok)
insert_data(9, '화사')
print(katok)
```


### 1.3 데이터 삭제 함수


```
katok = ["다현", "정연", "쯔위", "사나", "지효"]

def delete_data(position):
    if position < 0 or position > len(katok):
        print("데이터를 삭제할 범위를 벗어났습니다.")
        return

    klen = len(katok)
    katok[position] = None

    for i in range(position+1, klen):
        katok[i-1] = katok[i]
        katok[i] = None
    
    del(katok[klen-1])

delete_data(1)
print(katok)
delete_data(3)
print(katok)
```


### 1.4 완성코드


```
def add_data(frined):
    katok.append(None)
    klen = len(katok)
    katok[klen-1] = frined

def insert_data(position, friend):
    if position < 0 or position > len(katok):
        # '<' not supported between instances of 'str' and 'int'
        print("데이터를 삽입할 범위를 벗어났습니다.")
        return

    katok.append(None)
    klen = len(katok)

    for i in range(klen-1, position, -1):
        katok[i] = katok[i-1]
        katok[i-1] = None
    
    katok[position] = friend

def delete_data(position):
    if position < 0 or position > len(katok):
        print("데이터를 삭제할 범위를 벗어났습니다.")
        return

    klen = len(katok)
    katok[position] = None

    for i in range(position+1, klen):
        katok[i-1] = katok[i]
        katok[i] = None
    
    del(katok[klen-1])

## 전역 변수 선언 부분 ##
katok = []
select = -1 # 1: 추가, 2: 삽입, 3: 삭제, 4: 종료

## 메인코드 부분 ##
if __name__=="__main__":

    while(select != 4):
        select = int(input("선택하세요(1: 추가, 2: 삽입, 3: 삭제, 4: 종료)-->"))
        if (select==1):
            data = input('추가할 데이터--> ')
            add_data(data)
            print(katok)
        elif (select==2):
            pos = int(input('삽입할 위치--> '))
            data = input('추가할 데이터--> ')
            insert_data(pos, data)
            print(katok)
        elif (select==3):
            pos = int(input('삭제할 위치--> '))
            delete_data(pos)
            print(katok)
        elif (select==4):
            print(katok)
            exit
        else:
            print('1~4 중 하나를 입력하세요.')
            continue
```



## 2. 단순 연결 리스트(Singly Linked List)

- 노드(node) = 데이터(data) + 링크(link)
- 헤더(header) = 첫 번째 노드
- 링크(link) = 다음 데이터를 가리키는 포인터 변수
![image](https://github.com/rnasterofmysea/algorithm/assets/81907470/4859c241-6ff6-42a0-9ff2-eafcb4cae781)
![image](https://github.com/rnasterofmysea/algorithm/assets/81907470/44dd16f5-b486-495e-909a-8c286eda5c82)



### 2.1 노드 생성과 연결


```
class Node():
    def __init__(self):
        self.data = None
        self.link = None
```
```
def printNodes(start):                  # 매개변수로 시작 노드를 전달 받음
    current = start                     # 전달 받은 시작 노드를 현재 노드로 지정
    if current == None:                 # 노드에 데이터가 하나도 없는 연결 리스트인 경우 반환
        return
    print(current.data, end=' ')        # 현재 노드 출력
    while current.link != None:         # 노드의 링크가 빌 때까지 출력
        current = current.link
        print(current.data, end=' ')
    print()
    
## 전역 변수 선언 부분 ##
memory = []                             # 생성할 노드 저장할 메모리 준비
head, current, pre = None, None, None   # 시작 노드, 현재 노드, 이전 노드에 사용할 변수 준비
dataArray = ['다현', '정연', '쯔위', '사나', '지효']

## 메인 코드 부분 ##
if __name__ == "__main__":

    node = Node()
    node.data = dataArray[0]            # 첫 번째 노드 생성
    head = node
    memory.append(node)

    for data in dataArray[1:]:          # 두 번째 이후 노드
        pre = node                      # 현재 노드를 이전 노드로 저장함
        node = Node()                   # 새 노드 생성
        node.data = data                # 노드에 데이터를 넣음
        pre.link = node                 # 이전 노드 링크에 새 노드 대입
        memory.append(node)             # 새 노드를 메모리에 넣음

    printNodes(head)                    # 생성이 완료된 단순 연결 리스트 출력
```

### 2.2 노드 삽입 함수


```
def insertNode(findData, insertData):   # 매개 변수로 삽입할 위치를 찾을 데이터(findData), 삽입할 데이터(insertData)를 넘겨 받는다.
    global memory, head, current, pre

    if head.data == findData :          # 첫 번째 노드 삽입
        node = Node()
        node.data = insertData
        node.link = head
        head = node
        return

    current = head
    while current.link != None :        # 중간 노드 삽입
        pre = current
        current = current.link
        if current.data == findData:
            node = Node()
            node.data = insertData
            node.link = current
            pre.link = node
            return
    
    node = Node()                       # 마지막 노드 삽입
    node.data = insertData
    current.link = node
```


### 2.3 노드 삭제 함수


```
def deleteNode(deleteData):
    global memory, head, current, pre

    if head.data == deleteData:         # 첫 번째 노드 삭제
        current = head
        head = head.link
        del(current)
        return

    current = head                      # 첫 번째 외 노드 삭제
    while current.link != None:
        pre = current
        current = current.link
        if current.data == deleteData:
            pre.link = current.link
            del(current)
            return
```


### 2.4 노드 검색 함수


```
def findNode(findData):
    global memory, head, current, pre

    current = head
    if current.data == findData:
        return current
    while current.link != None:
        current = current.link
        if current.data == findData:
            return current
    return Node()       # 빈 노드 반환
```

## 3. 원형 연결 리스트(Circular Linked List)

![image](https://github.com/rnasterofmysea/algorithm/assets/81907470/01ff12ad-e505-4b72-b863-98dc54517705)

### 3.1 노드 생성


```
## 클래스와 함수 선언 부분 ##
class Node():
    def __init__(self):
        self.data = None
        self.link = None

def printNodes(start):                      # 시작 노드 전달 받음
    current = start                         # 현재 노드로 지정
    if current.link == None:                # 노드에 데이터가 하나도 없는 연결 리스트인 경우
        return                              # 반환한다
    print(current.data, end=' ')            # 현재 노드 출력
    while current.link != start:            # 현재 노드의 링크가 전달 받은 노드(=첫 번째 노드)가 아닐 때까지 반복
        current = current.link              # 현재 노드의 링크가 첫 번째 노드라면 원형 연결 리스트에서는 마지막 노드를 의미함
        print(current.data, end=' ')
    print()

## 전역 변수 선언 부분 ##
memory = []
head, current, pre = None, None, None
dataArray = ['다현', '정연', '쯔위', '사나', '지효']

## 메인 코드 부분 ##
if __name__ == "__main__":

    node = Node()
    node.data = dataArray[0]
    head = node
    memory.append(node)

    for data in dataArray[1:]:
        pre = node
        node = Node()
        node.data = data
        pre.link = node
        node.link = head
        memory.append(node)

    printNodes(head)
```


### 3.2 노드 삽입


```
def insertNode(findData, insertData):       # 첫 번째 노드 삽입
    global memory, head, current, pre      

    if head.data == findData:
        node = Node()
        node.data = insertData
        node.link = head
        last = head                         # 마지막 노드를 첫 번째 노드로 우선 지정
        while last.link != head:            # 마지막 노드의 링크가 head가 아닐 때 -> 마지막 노드를 찾으면 반복 종료
            last = last.link                # last를 다음 노드로 변경
        last.link = node                    # 마지막 노드의 링크에서 새 노드 지정
        head = node
        return

    current = head
    while current.link != head:             # 중간 노드 삽입
        pre = current
        current = current.link
        if current.link == findData:
            node = Node()
            node.data = insertData
            node.link = current
            pre.link = node
            return
        
    node = Node()                           # 마지막 노드 삽입 -> 찾을 데이터가 없는 경우(while문이 종료되고)
    node.data = insertData
    current.link = node                     # 새 노드 생성 후 현재(current) 노드 링크를 새 노드로 지정
    node.link = head  
```


### 3.3 데이터 삭제


```
def deleteNode(deleteData):
    global memory, head, current, pre

    if head.data == deleteData:             # 삭제할 노드가 첫 번째 노드일 때
        current = head                      # 현재 노드를 헤드 노드와 동일하게 만들기
        head = head.link                    # head 노드를 다음 노드로 변경
        last = head                        
        while last.link != current:         # 마지막 노드를 찾으면 반복 종료 
            last = last.link                # last를 다음 노드로 변경
        last.link = head                    # 마지막 노드의 링크에 head가 가리키는 노드 지정
        del(current)
        return

    current = head                          # 첫 번째 외 노드 삭제
    while current.link != head:
        pre = current
        current = current.link
        if current.data == deleteData:      # 중간 노드를 찾았을 때
            pre.link = current.link
            del(current)
            return
```


### 3.4 데이터 검색


```
def findNode(findData):                     # 노드를 검색하는 함수
    global memory, head, current, pre       # 전역 변수 가져오기

    current = head                          # 현재 노드를 head로 지정
    if current.data == findData:            # 현재 노드의 데이터가 찾는 데이터라면
        return current                      # current 반환
    while current.link != head:             # 노드가 끝날 때까지 반복
        current = current.link              # 현재 노드에서 다음 노드로 이동
        if current.data == findData:        # 현재 노드의 데이터가 찾는 데이터라면
            return current                  # current 반환
    return Node()                           # 빈 노드 반환
```


## 4. 이진트리(Binary Tree)

- 트리(Tree) 자료구조: 트리의 거꾸로 뒤집어 놓은 형태
- 뿌리(root): 트리의 맨 위
- 레벨: 트리에서 아래로 내려올수록 레벨이 1씩 증가함
- 노드(Node): 트리에서 각 위치를 노드라고 함
- 에지(edge): 노드끼리 연결되어 있는 선
- 차수(degree): 노드가 갖고 있는 자식 노드의 수
- 리프(leaf): 자식 노드가 없는 노드

![image](https://github.com/rnasterofmysea/algorithm/assets/81907470/7e1816fb-b3d2-4555-ad21-8245b63a3e38)


### 4.1 이진트리의 종류

#### 4.1.1 포화 이진 트리(full binary tree)

![image](https://github.com/rnasterofmysea/algorithm/assets/81907470/e4330311-b269-48f3-99c5-c3f1ca21149b)

#### 4.1.2 완전 이진 트리(complete binary tree)

![image](https://github.com/rnasterofmysea/algorithm/assets/81907470/c7964147-66d0-4262-a1ef-8e5307e8a6fd)

#### 4.1.3 편향 이진 트리(skewed binary tree)

![image](https://github.com/rnasterofmysea/algorithm/assets/81907470/146d7471-95f7-482a-84a3-c3c59fce41fe)

### 4.2 이진 트리 생성


```
class TreeNode():
    def __init__(self):
        self.left = None
        self.right = None
        self.data = None
        
node1= TreeNode()
node1.data = '화사'

node2= TreeNode()
node2.data = '솔라'
node1.left = node2

node3= TreeNode()
node3.data = '문별'
node1.right = node3

node4= TreeNode()
node4.data = '휘인'
node2.left = node4

node5= TreeNode()
node5.data = '쯔위'
node2.right = node5

node6= TreeNode()
node6.data = '선미'
node3.left = node6

print(node1.data, end=' ')
print()
print(node1.left.data, node1.right.data, end=' ')
print()
print(node1.left.left.data, node1.left.right.data, node1.right.left.data, end=' ')
```


### 4.2 이진 트리 삽입


```
class TreeNode():
    def __init__(self):
        self.left = None
        self.data = None
        self.right = None
        
## 전역 변수 선언 부분 ##
memory = []
root = None
nameAry = ['블랙핑크', '레드벨벳', '마마무', '에이핑크', '걸스데이', '트와이스']

## 메인 코드 부분 ##
node = TreeNode()               # 이름의 배열의 첫 번째 데이터를 루트 노드로 생성하고 메모리 공간에 넣는다.
node.data = nameAry[0]
root = node
memory.append(node)

for name in nameAry[1:]:
    
    node = TreeNode()           # 새 노드 생성
    node.data = name
    
    current = root              # 항상 루트 노트부터 시작한다. 즉, 현재 작업 노드는 항상 루트 노드부터 진행한다.
    while True:
        if name < current.data:
            if current.left == None:
                current.left = node
                break
            current = current.left
        else:
            if current.right == None:
                current.right = node
                break
            current = current.right
    
    memory.append(node)
    
print("이진 탐색 트리 구성 완료!")
```


### 4.3 데이터 삭제


```
## 함수 선언 부분 ##
class TreeNode():
    def __init__(self):
        self.left = None
        self.data = None
        self.right = None
        
## 전역 변수 선언 부분 ##
memory = []
root = None
nameAry = ['블랙핑크', '레드벨벳', '마마무', '에이핑크', '걸스데이', '트와이스']

## 메인 코드 부분 ##
node = TreeNode()               # 이름의 배열의 첫 번째 데이터를 루트 노드로 생성하고 메모리 공간에 넣는다.
node.data = nameAry[0]
root = node
memory.append(node)

for name in nameAry[1:]:
    
    node = TreeNode()           # 새 노드 생성
    node.data = name
    
    current = root              # 항상 루트 노트부터 시작한다. 즉, 현재 작업 노드는 항상 루트 노드부터 진행한다.
    while True:
        if name < current.data:
            if current.left == None:
                current.left = node
                break
            current = current.left
        else:
            if current.right == None:
                current.right = node
                break
            current = current.right
    
    memory.append(node)
    
deleteName = '마마무'

current = root
parent = None
while True:
    if deleteName == current.data:
        
        if current.left == None and current.right == None:
            if parent.left == current:
                parent.left = None
            else:
                parent.right = None
            del(current)
            
        elif current.left != None and current.right == None:
            if parent.left == current:
                parent.left = current.left
            else:
                parent.right = current.left
            del(current)
            
        elif current.left == None and current.right != None:
            if parent.left == current:
                parent.left = current.right
            else:
                parent.right = current.right
            del(current)
            
        print(deleteName, '이(가) 삭제됨')
        break
    
    elif deleteName < current.data:
        if current.left == None:
            print(deleteName, '이(가) 트리에 없음')
            break
        parent = current
        current = current.left
    else:
        if current.right == None:
            print(deleteName, '이(가) 트리에 없음')
            break
        parent = current
        current = current.right
```


## 순열 & 조합

![image](https://github.com/rnasterofmysea/algorithm/assets/81907470/d2996e22-2119-4eb5-8905-47e79442983a)

![image](https://github.com/rnasterofmysea/algorithm/assets/81907470/d913c7b1-25e8-4e59-9fb0-9bad1f6b7c9c)
