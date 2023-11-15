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