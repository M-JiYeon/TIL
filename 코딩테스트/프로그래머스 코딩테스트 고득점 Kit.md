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

---

## 힙(Heap)

### 더 맵게

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42626

```py
import heapq as hq

def solution(scoville, K):
    hq.heapify(scoville)
    answer = 0
    while True:
        first = hq.heappop(scoville)
        if first >= K:
            break
        if len(scoville) == 0:
            return -1
        second = hq.heappop(scoville)
        hq.heappush(scoville, first + second*2)
        answer += 1  

    return answer
```

### 디스크 컨트롤러

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42627

```py
import heapq

def solution(jobs):
    answer, now, i = 0, 0, 0
    start = -1 
    heap = []
    
    while i < len(jobs):
        for j in jobs:
            if start < j[0] <= now:
                heapq.heappush(heap, [j[1], j[0]])
        
        if len(heap) > 0:
            cur = heapq.heappop(heap)
            start = now
            now += cur[0]
            answer += now - cur[1]
            i +=1
        else:
            now += 1
                
    return answer // len(jobs)
```

### 이중우선순위큐

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42628

```py
import heapq

def solution(operations):
    answer = []
    heap = []

    for data in operations:
        if data[0] == "I":
            heapq.heappush(heap, int(data[2:]))
        else:
            if len(heap) == 0:
                pass
            elif data[2] == "-":
                heapq.heappop(heap)
            else:
                heap = heapq.nlargest(len(heap), heap)[1:]
                heapq.heapify(heap)

    if heap:
        answer.append(max(heap))
        answer.append(min(heap))
    else:
        answer.append(0)
        answer.append(0)
    
    return answer
```

---

## 정렬

### K번째수

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42748

```py
def solution(array, commands):
    answer = []
    for c in commands:
        i,j,k = c
        answer.append( sorted(array[i-1:j])[k-1])
    return answer

def solution(array, commands):
    return list(map(lambda x:sorted(array[x[0]-1:x[1]])[x[2]-1], commands))
```

### 가장 큰 수

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42746

```py
def solution(numbers):
    s = list(map(str, numbers))
    s.sort(key=lambda x: x*3, reverse=True)
    return str(int(''.join(s)))
```

### H-Index

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42747

```py
def solution(citations):
    citations.sort(reverse=True)
    
    for i in range(len(citations)):
        if(citations[i] < i+1):
            return i

    return len(citations)
```

---

## 완전탐색

### 최소직사각형

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/86491

```py
def solution(sizes):
    w = []
    h = []
    for i in range(len(sizes)):
        if sizes[i][0] >= sizes[i][1]:
            w.append(sizes[i][0])
            h.append(sizes[i][1])
        else:
            h.append(sizes[i][0])
            w.append(sizes[i][1])
    return max(w) * max(h)

def solution(sizes):
    return max(max(x) for x in sizes) * max(min(x) for x in sizes)
```

### 모의고사

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42840

```py
def solution(answers):
    p = [[1, 2, 3, 4, 5],
         [2, 1, 2, 3, 2, 4, 2, 5],
         [3, 3, 1, 1, 2, 2, 4, 4, 5, 5]]
    s = [0] * len(p)

    for q, a in enumerate(answers):
        for i, v in enumerate(p):
            if a == v[q % len(v)]:
                s[i] += 1
    return [i + 1 for i, v in enumerate(s) if v == max(s)]
```

### 소수 찾기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42839

```py
from itertools import permutations

def is_prime_number(x) :
    if x < 2 :
        return False
    for i in range(2, x) :
        if x % i == 0 :
            return False      
    return True

def solution(numbers):
    answer = 0
    nums = []
    
    for i in range(1, len(numbers)+1) :
        nums.append(list(set(map(''.join, permutations(numbers, i)))))
    per = list(set(map(int, set(sum(nums, [])))))
    
    for p in per :
        if is_prime_number(p) == True :
            answer += 1

    return answer
```

### 카펫

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42842

```py
def solution(brown, yellow):
    answer = []
    total = brown + yellow
    for i in range(1,total+1):
        if (total / i) % 1 == 0:
            a = total / i
            if a >= i:
                if 2*a + 2*i == brown + 4:
                    return [a,i]        
    return answer
```

### 피로도

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/87946

```py
from itertools import permutations

def solution(k, dungeons):
    answer = 0
    for i in permutations(dungeons, len(dungeons)):
        hp = k
        count = 0 
        for j in i:
            if hp >= j[0]:
                hp -= j[1]
                count += 1
            if count > answer:
                answer = count
    return answer
```

### 전력망을 둘로 나누기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/86971

```py
def solution(n, wires):
    answer = n
    for sub in (wires[i+1:] + wires[:i] for i in range(len(wires))):
        s = set(sub[0])
        [s.update(v) for _ in sub for v in sub if set(v) & s]
        answer = min(answer, abs(2 * len(s) - n))
    return answer

from collections import deque
def bfs(node, tree, visited, wire, cnt):
    queue = deque()
    queue.append([node, tree, visited, wire])
    visited[node] = True
    while queue:
        node, tree, visited, wire = queue.popleft()
        cnt += 1
        for i in tree[node]:
            if not ((node == wire[0] and i == wire[1]) or (node == wire[1] and i == wire[0])):
                if not visited[i]:
                    visited[i] = True
                    queue.append([i, tree, visited, wire])
    return cnt

def solution(n, wires):
    answer = 1e9
    tree = [[] for _ in range(n + 1)]
    for wire in wires:
        a, b = wire
        tree[a].append(b)
        tree[b].append(a)
    for wire in wires:
        visited = [False] * (n + 1)
        temp = []
        for i in range(1, n + 1):
            if not visited[i]:
                cnt = bfs(i, tree, visited, wire, 0)
                temp.append(cnt)
        answer = min(answer, abs(temp[0] - temp[1]))
    return answer
```

### 모음 사전

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/84512

```py
def solution(word):
    answer = 0
    dic = ['A', 'E', 'I', 'O', 'U']
    li = [5**i for i in range(len(dic))]
    
    for i in range(len(word)-1,-1,-1):
        idx = dic.index(word[i])
        for j in range(5-i):
            answer += li[j]*idx
        answer+=1
    return answer
```

---

## 탐욕법(Greedy)

### 체육복

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42862

```py
def solution(n, lost, reserve):
    r = [i for i in sorted(reserve) if i not in lost]
    l = [i for i in sorted(lost) if i not in reserve]
    for i in r:
        if i-1 in l:
            l.remove(i-1)
        elif i+1 in l:
            l.remove(i+1)
    return n - len(l)
```

### 조이스틱

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42860

```py
def solution(name):
    answer = 0
    min_move = len(name) - 1
    
    for i, char in enumerate(name):
        answer += min(ord(char) - ord('A'), ord('Z') - ord(char) + 1)
        next = i + 1
        while next < len(name) and name[next] == 'A':
            next += 1
        min_move = min([min_move, 2 *i + len(name) - next, i + 2 * (len(name) -next)])
        
    answer += min_move
    return answer
```

### 큰 수 만들기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42883

```py
def solution(number, k):
    answer = []

    for i in number:
        if len(answer) == 0:
            answer.append(i)
            continue
        if k > 0:
            while answer[-1] < i:
                answer.pop()
                k -= 1
                if len(answer) == 0 or k <= 0:
                    break
        answer.append(i)

    answer = answer[:-k] if k > 0 else answer
    return ''.join(answer)
```

### 구명보트

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42885

```py
def solution(people, limit):
    answer = 0
    people.sort()

    a = 0
    b = len(people) - 1
    while a < b :
        if people[b] + people[a] <= limit :
            a += 1
            answer += 1
        b -= 1
    return len(people) - answer
```

### 섬 연결하기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42861

```py
def solution(n, costs):
    answer = 0
    costs.sort(key = lambda x: x[2]) 
    link = set([costs[0][0]])

    while len(link) != n:
        for v in costs:
            if v[0] in link and v[1] in link:
                continue
            if v[0] in link or v[1] in link:
                link.update([v[0], v[1]])
                answer += v[2]
                break
                
    return answer
```

### 단속카메라

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42884

```py
def solution(routes):
    answer = 0
    routes.sort(key=lambda x: x[1])
    camera = -30001

    for route in routes:
        if camera < route[0]:
            answer += 1
            camera = route[1]
    return answer
```

---

## 동적계획법(Dynamic Programming)

### N으로 표현

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42895

```py
def solution(N, number):
    dp = [set() for i in range(9)]
    for i in range(1, 9):
        dp[i].add(int(str(N)*i))
        for j in range(i//2 + 1):
            for first in dp[j]:
                for second in dp[i-j]:
                    dp[i].add(first + second)
                    dp[i].add(first - second)
                    dp[i].add(second - first)
                    dp[i].add(first * second)
                    if second != 0 :
                        dp[i].add(first // second)
                    if first != 0 :
                        dp[i].add(second // first)
                    
        if number in dp[i]:
            return i
    return -1
```

### 정수 삼각형

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/43105

```py
def solution(triangle):
    answer = 0
    for i in range(1, len(triangle)):
        for j in range(len(triangle[i])):
            if j == 0:
                triangle[i][j] += triangle[i-1][0]
            elif j == len(triangle[i])-1:
                triangle[i][j] += triangle[i-1][-1]
            else:
                triangle[i][j] += max(triangle[i-1][j], triangle[i-1][j-1])
    return max(triangle[-1])
```

### 등굣길

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42898

```py
def solution(m, n, puddles):
    dp = [[0] * (m + 1) for _ in range(n + 1)] 
    dp[1][1] = 1
    
    for i, j in puddles: 
        dp[j][i] = -1
        
    for i in range(1, n + 1):
        for j in range(1, m + 1):
            if dp[i][j] == -1: 
                dp[i][j] = 0
                continue 
            dp[i][j] += (dp[i - 1][j] + dp[i][j - 1]) % 1000000007
            
    return(dp[n][m])
```

### 사칙연산

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/1843

```py
def solution(arr):
    M, m = {}, {}
    nums = [int(x) for x in arr[::2]]
    ops = [x for x in arr[1::2]]
    
    for i in range(len(nums)):
        M[(i, i)] = nums[i]
        m[(i, i)] = nums[i]
    
    for d in range(1, len(nums)):
        for i in range(len(nums)):
            j = i + d
            if j >= len(nums):
                continue
            
            maxcandidates, mincandidates = [], []
            for k in range(i+1, j+1):
                if ops[k-1] == '-':
                    mx = M[(i, k-1)] - m[(k, j)]
                    mn = m[(i, k-1)] - M[(k, j)]
                    maxcandidates.append(mx)
                    mincandidates.append(mn)
                else:
                    mx = M[(i, k-1)] + M[(k, j)]
                    mn = m[(i, k-1)] + m[(k, j)]
                    maxcandidates.append(mx)
                    mincandidates.append(mn)
            
            M[(i, j)] = max(maxcandidates)
            m[(i, j)] = min(mincandidates)
                    
    return M[(0, len(nums) - 1)]
```

### 도둑질

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42897

```py
def solution(money):
    dp1 = [0] * len(money)
    dp1[0] = money[0]
    dp1[1] = max(money[0], money[1])

    for i in range(2, len(money)-1):
        dp1[i] = max(dp1[i-1], money[i]+dp1[i-2])

    dp2 = [0] * len(money)
    dp2[0] = 0
    dp2[1] = money[1]

    for i in range(2, len(money)):
        dp2[i] = max(dp2[i-1], money[i]+dp2[i-2])

    return max(max(dp1), max(dp2))
```

## 깊이/너비 우선 탐색(DFS/BFS)

### 타겟 넘버

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/43165

```py
def solution(numbers, target):
    answer = 0
    queue = [[numbers[0],0], [-1*numbers[0],0]]
    n = len(numbers)
    while queue:
        temp, idx = queue.pop()
        idx += 1
        if idx < n:
            queue.append([temp+numbers[idx], idx])
            queue.append([temp-numbers[idx], idx])
        else:
            if temp == target:
                answer += 1
    return answer
```

### 네트워크

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/43162

```py
def DFS(n, computers, com, visited):
    visited[com] = True
    for connect in range(n):
        if connect != com and computers[com][connect] == 1:
            if visited[connect] == False:
                DFS(n, computers, connect, visited)

def solution(n, computers):
    answer = 0
    visited = [False for i in range(n)]
    for com in range(n):
        if visited[com] == False:
            DFS(n, computers, com, visited)
            answer += 1
    return answer
```

### 게임 맵 최단거리

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/1844

```py
from collections import deque
def solution(maps):
    answer = 0
    dx = [-1,1,0,0]
    dy = [0,0,-1,1]

    queue = deque()
    queue.append((0,0))	

    while queue:
        x, y = queue.popleft()
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            N = len(maps)
            M = len(maps[0])
            if 0<=nx<N and 0<=ny<M and maps[nx][ny]==1:
                maps[nx][ny] = maps[x][y]+1
                queue.append((nx,ny))
    answer = maps[N-1][M-1]
    
    if answer ==1:
        answer = -1
    return answer
```

### 단어 변환

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/43163

```py
from collections import deque

def solution(begin, target, words):
    answer = 0
    q = deque()
    q.append([begin, 0])
    V = [ 0 for i in range(len(words))]
    while q:
        word, cnt = q.popleft()
        if word == target:
            answer = cnt
            break        
        for i in range(len(words)):
            temp_cnt = 0
            if not V[i]:
                for j in range(len(word)):
                    if word[j] != words[i][j]:
                        temp_cnt += 1
                if temp_cnt == 1:
                    q.append([words[i], cnt+1])
                    V[i] = 1
                    
    return answer
```

### 아이템 줍기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/87694

```py
from collections import deque

def solution(rectangle, characterX, characterY, itemX, itemY):
    answer = 0
    field = [[-1] * 102 for i in range(102)]
    
    for r in rectangle:
        x1, y1, x2, y2 = map(lambda x: x*2, r)
        for i in range(x1, x2+1):
            for j in range(y1, y2+1):
                if x1 < i < x2 and y1 < j < y2:
                    field[i][j] = 0
                elif field[i][j] != 0:
                    field[i][j] = 1
                    
    dx = [-1, 1, 0, 0]
    dy = [0, 0, -1, 1]
    
    q = deque()
    q.append([characterX * 2, characterY * 2])
    visited = [[1] * 102 for i in range(102)]
    visited[characterX * 2][characterY * 2] = 0
    
    while q:
        x, y = q.popleft()
        if x == itemX * 2 and y == itemY * 2:
            answer = visited[x][y] // 2
            break
        for k in range(4):
            nx = x + dx[k]
            ny = y + dy[k]
            if field[nx][ny] == 1 and visited[nx][ny] == 1:
                q.append([nx, ny])
                visited[nx][ny] = visited[x][y] + 1
    
    return answer
```
### 여행경로

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/43164

```py
from collections import deque

def solution(tickets):
    answer = []
    q = deque()
    q.append(("ICN",["ICN"], []))
    
    while q:
        airport, path, used = q.popleft()

        if len(used) == len(tickets):
            answer.append(path)
        
        for idx, ticket in enumerate(tickets):
            if ticket[0] == airport and not idx in used:
                q.append((ticket[1], path+[ticket[1]], used+[idx]))
                
    
    answer.sort()

    return answer[0]
```

### 퍼즐 조각 채우기

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/84021

```py
import copy

def solution(game_board, table):
    n = len(game_board)
    answer = 0
    blank = []
    for i in range(n):
        for j in range(n):
            if game_board[i][j] == 0:
                blank.append(dfs(game_board, i, j, [0, 0], n, 0))

    for k in range(4):
        table = rotate(table)
        copy_table = copy.deepcopy(table)
        for i in range(n):
            for j in range(n):
                if copy_table[i][j] == 1:
                    block = dfs(copy_table, i, j, [0, 0], n, 1)
                    if block in blank:
                        blank.remove(block)
                        answer += len(block)
                        table = copy.deepcopy(copy_table)
                    else:
                        copy_table = copy.deepcopy(table)
    return answer


def dfs(board, x, y, position, n, num):
    dx = [-1, 0, 1, 0]
    dy = [0, 1, 0, -1]

    result = [position]

    board[x][y] = 2 

    for i in range(4):
        px = x + dx[i]
        py = y + dy[i]

        if 0 <= px and px < n and 0 <= py and py < n:
            if board[px][py] == num:
                result += dfs(board, px, py, [position[0] + dx[i], position[1] + dy[i]], n, num)

    return result

def rotate(table):
    n = len(table)
    rotated = [[0] * n for _ in range(n)]

    for i in range(n):
        for j in range(n):
            rotated[j][n - i - 1] = table[i][j]

    return rotated
```

## 이분탐색

### 입국심사

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/43238

```py
def solution(n, times):
    answer = 0
    leng = len(times)
    left = 1
    right = (leng+1) * max(times)

    while left <= right:
        mid = (left + right) // 2

        count = 0
        for time in times:
            count += mid // time
            if count >= n: break

        if count >= n:
            answer = mid
            right = mid - 1
        elif count < n:
            left = mid + 1

    return answer
```

### 징검다리

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/43236

```py
def solution(distance, rocks, n):
    answer = 0
    left, right = 0, distance
    rocks.append(distance)
    rocks.sort() 
    
    while left <= right:
        mid = (left + right) // 2
        current, remove =  0, 0
        min_distance = float('inf')

        for rock in rocks:
            dis = rock - current
            if dis < mid:
                remove += 1
            else:
                current = rock
                min_distance = min(min_distance, dis)
                
        if remove > n:
            right = mid - 1
        else:
            answer = min_distance
            left = mid + 1
        
    return answer
```

## 그래프

### 가장 먼 노드

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/49189

```py
def solution(n, edge):
    adj = [[] for _ in range(n + 1)]
    for v1, v2 in edge:
        adj[v1].append(v2)
        adj[v2].append(v1)
    
    answer = [0 for _ in range(n + 1)]
    answer[1] = 1
    
    queue = [1]
    
    while queue:
        cur = queue.pop(0)
        for dest in adj[cur]:
            if not answer[dest]:
                answer[dest] = answer[cur] + 1
                queue.append(dest)
        
    return answer.count(max(answer))
```

### 순위

---

-   링크 : https://school.programmers.co.kr/learn/courses/30/lessons/49191

```py
def solution(n, results):
    answer = 0
    board = [[0]*n for _ in range(n)]
    
    for a,b in results:
        board[a-1][b-1] = 1
        board[b-1][a-1] = -1
        
    for k in range(n):
        for i in range(n):
            for j in range(n):
                if i == j or board[i][j] in [1,-1]:
                    continue
                if board[i][k] == board[k][j] == 1:
                    board[i][j] = 1
                    board[j][i] = board[k][i] = board[j][k] = -1
    for row in board:
        if row.count(0) == 1:
            answer += 1
    return answer
```