# 프로그래머스 코딩테스트 고득점 Kit

## 해시

### 완주하지 못한 선수

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42576

```py
def solution(participant, completion):
    a = sorted(participant)
    b = sorted(completion)
    for i in range(len(completion)):
        if a[i] != b[i]:
            return a[i]
    return a[-1]

import collections
def solution(participant, completion):
    answer = collections.Counter(participant) - collections.Counter(completion)
    return list(answer.keys())[0]
```

### 폰켓몬

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/1845

```py
def solution(nums):
    return min(len(set(nums)), int(len(nums) / 2))
```

### 전화번호 목록

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42577

```py
def solution(phone_book):
    answer = True
    hash_map = {}
    for phone_number in phone_book:
        hash_map[phone_number] = 1
    for phone_number in phone_book:
        temp = ""
        for number in phone_number:
            temp += number
            if temp in hash_map and temp != phone_number:
                answer = False
    return answer

def solution(phoneBook):
    phoneBook = sorted(phoneBook)

    for p1, p2 in zip(phoneBook, phoneBook[1:]):
        if p2.startswith(p1):
            return False
    return True
```

### 의상

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42578

```py
def solution(clothes):
    hash_map = {}
    for clothe, type in clothes:
        hash_map[type] = hash_map.get(type, 0) + 1    
    answer = 1
    for type in hash_map:   
        answer *= (hash_map[type] + 1)
    return answer - 1
```

### 베스트앨범

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42579

```py
def solution(genres, plays):
    answer = []

    dic1 = {}
    dic2 = {}

    for i, (g, p) in enumerate(zip(genres, plays)):
        if g not in dic1:
            dic1[g] = [(i, p)]
        else:
            dic1[g].append((i, p))

        if g not in dic2:
            dic2[g] = p
        else:
            dic2[g] += p

    for (k, v) in sorted(dic2.items(), key=lambda x:x[1], reverse=True):
        for (i, p) in sorted(dic1[k], key=lambda x:x[1], reverse=True)[:2]:
            answer.append(i)

    return answer
```

---

## 스택/큐

### 같은 숫자는 싫어

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/12906

```py
def solution(arr):
    answer = []
    answer.append(arr[0])
    
    for i in arr[1:]:
        if i != answer[-1]:
            answer.append(i)
    
    return answer
```

### 기능개발

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42586

```py
def solution(progresses, speeds):
    Q=[]
    for p, s in zip(progresses, speeds):
        if len(Q)==0 or Q[-1][0]<-((p-100)//s):
            Q.append([-((p-100)//s),1])
        else:
            Q[-1][1]+=1
    return [q[1] for q in Q]
```

### 올바른 괄호

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/12909

```py
def solution(s):
    answer = []
    
    for i in s:
        if i == '(':
            answer.append(i)
        else:
            if answer == []:
                return False
            else:
                answer.pop()
    
    return len(answer) == 0
```

### 프로세스

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42587

```py
def solution(priorities, location):
    queue =  [(i,p) for i,p in enumerate(priorities)]
    answer = 0
    while True:
        cur = queue.pop(0)
        if any(cur[1] < q[1] for q in queue):
            queue.append(cur)
        else:
            answer += 1
            if cur[0] == location:
                return answer
```

### 다리를 지나는 트럭

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42583

```py
from collections import deque
def solution(bridge_length, weight, truck_weights):
    time = 0
    bridge = deque([0] * bridge_length)
    truck_weights = deque(truck_weights)
    currentWeight = 0

    while len(truck_weights)!=0:
        time+=1
        currentWeight -= bridge.popleft()

        if currentWeight + truck_weights[0] <= weight:
            currentWeight+= truck_weights[0]
            bridge.append(truck_weights.popleft())
        else: 
            bridge.append(0)
            
    time += bridge_length
    
    return time
```

### 주식가격

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42584

```py
from collections import deque

def solution(prices):
    answer = []
    queue = deque(prices)
    
    while queue:
        price = queue.popleft()
        sec = 0
        for q in queue:
            sec += 1
            if price > q:
                break 
        answer.append(sec)        
    return answer
```