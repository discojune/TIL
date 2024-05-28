# 99클럽 코테 스터디 9일차 TIL : Brute Force(완전 탐색)

## 카펫
프로그래머스 문제 링크:
- https://school.programmers.co.kr/learn/courses/30/lessons/42842


## 풀이 1. 완전 탐색

### 🤔 시행 착오
brown 격자의 최소값은 8이고, yellow 격자의 최소값은 1이므로 가장 기본적인 카펫 형태는 [3, 3] 격자 모양이다.
따라서 세로의 최소 길이를 3으로 하고, brown과 yellow를 더한 값인 카펫의 넓이가 되게 하는 가로 길이를 찾는 방법으로 알고리즘을 생각했다.

최대공약수를 구하는 알고리즘을 참고하여 3의 배수, 4의 배수의 세로 길이를 구하고, 

넓이를 만족하는 가로 길이 (넓이가 세로 길이로 나눠 떨어질 때)가 있으면 두 가로, 세로 길이를 반환한다.

하지만 이 알고리즘은 절반의 문제를 실패했다.


### 💡 새롭게 알게 된 것
이 문제의 핵심은 노란 격자를 갈색 격자가 1줄로 감싸는 모양이라는 것이다.

> Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 노란색으로 칠해져 있고 테두리 1줄은 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다.

따라서 기존 알고리즘에서 ```(카펫의 가로 길이 - 2) * (카펫의 세로 길이 - 2) == (노란 격자의 갯수)```를 만족해야만 카펫의 길이를 구할 수 있었다.

이를 기존 알고리즘에 적용하여 전 문제를 통과할 수 있었다.
### 🎉 풀이 코드
```python
def solution(brown, yellow):
    def recursive_GCM(a, b, s):
        div, mod = divmod(a, b)
        
        if div == 0:
            return s - 1 if s != 1 else 1
        
        return recursive_GCM(div, b, s + 1)    
    
    total_tiles = brown + yellow
    
    min_length = 3
    step = 0
    
    while True:
        
        step = recursive_GCM(total_tiles, min_length, step)

        length_1 = min_length * step
        
        div, mod = divmod(total_tiles, length_1)
        length_2 = div
        
        if mod == 0 and (length_1 - 2)*(length_2 - 2) == yellow:
            
            answer = [max(length_1, length_2), min(length_1, length_2)]
            
            return answer
        
        else:
            min_length += 1
            step = 0

```

### 🏃 studying with...
#99클럽 #코딩테스트 준비 #개발자 취업 #항해99 #TIL
![til_thumbnail](./img/thmb_python.png)