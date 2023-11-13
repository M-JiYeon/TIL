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