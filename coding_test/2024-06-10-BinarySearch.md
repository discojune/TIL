# 99클럽 코테 스터디 22일차 TIL : 이분 탐색(Binary Search)

## 입국심사
프로그래머스 문제 링크:
- https://school.programmers.co.kr/learn/courses/30/lessons/43238


## 풀이 1. 이분 탐색

### 🤔 시행 착오
오늘은 이분 탐색에 대한 개념을 이해하는 문제였다.

처음에는 이분 탐색 풀이법을 몰라서 n명의 입국 심사 시간을 모두 살펴보는 코드를 생각했지만, 예제는 통과해도 제출 시에는 실패하고 시간 초과가 걸렸다.

### 💡 새롭게 알게 된 것
이 문제의 핵심은 **최선의 시간과 최악의 시간의 중간 시간일 때** 심사관이 심사할 수 있는 사람의 수가 주어진 값 n이 되는지 비교하는 것이다.

n명보다 초과된다면 ```중간 시간 - 1```, n명보다 미만이면 ```중간 시간 + 1```을 하여 n명이 되는 지점을 찾으면 시간 복잡도가 작은 풀이가 가능하다.

### 📚 참고 풀이 코드
```python
def solution(n, times):
    answer = 0

    left, right = 1, max(times) * n
    while left <= right:
        mid = (left+ right) // 2
        people = 0
        for time in times:
            people += mid // time
            if people >= n:
                break
        
        if people >= n:
            answer = mid
            right = mid - 1

        elif people < n:
            left = mid + 1
            
    return answer

```

### 🏃 studying with...
#99클럽 #코딩테스트 준비 #개발자 취업 #항해99 #TIL
![til_thumbnail](./img/thmb_python.png)