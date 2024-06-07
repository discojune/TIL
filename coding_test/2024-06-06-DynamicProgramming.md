# 99클럽 코테 스터디 19일차 TIL : 동적계획법(Dynamic Programming)

## Count Sorted Vowel Strings
리트코드 문제 링크:
- https://leetcode.com/problems/count-sorted-vowel-strings/description/


## 풀이 1. 동적계획법
> 동적 계획법은 하나의 큰 문제를 여러 개의 작은 문제로 나누고, 작은 문제를 해결한 결과를 저장하여 큰 문제를 해결할 때 사용하는 문제 해결 패러다임이다.
- 참고: https://80000coding.oopy.io/60c3d4d3-f569-4b47-bdde-9a65d30f3bc5

### 🤔 시행 착오
이전 단계의 글자 수를 저장하고 다음 단계에서 한 글자씩 추가하는 방법을 통해 문제를 풀었다.
시간 초과를 막기 위해 글자는 사전식 순서를 만족해야 하므로 이전 단계의 단어의 마지막 글자보다 큰 글자는 건너뛰도록 하여 시간 초과 없이 문제를 풀 수 있었다.

하지만, 다른 리트코드의 문제 풀이들보다 시간, 공간 복잡도가 높은 코드여서 개선이 필요했다.

### 😅 개선이 필요한 풀이 코드
```python
class Solution:
    def countVowelStrings(self, n: int) -> int:

        vowels = ["a", "e", "i", "o", "u"]

        result = []
        for _ in range(n):
            
            temp = []
            if not result:
                for i, vowel in enumerate(vowels):
                    temp.append(vowel)

                result = temp

                continue

            for mem_string in result:
                for vowel in vowels:
                    if mem_string[-1] < vowel:
                        continue
                        
                    string = mem_string + vowel
                    temp.append(string)

            result = temp

        return len(result)

```

### 💡 새롭게 알게 된 것
모음으로 이루어진 단어의 갯수를 구하는 문제이므로 단어에 갯수에 대한 동적계획법을 사용하면 더 빠르게 푸는 것이 정도였다.

[Tabulation 방식의 리트코드 해설](https://leetcode.com/problems/count-sorted-vowel-strings/solutions/918760/dynamic-programming-python-100-explanation-code/)

코딩테스트는 문제를 잘 이해하는 것이 중요함을 다시 한번 배웠다...

### 📚 참고 풀이 코드
```python
class Solution:
    def countVowelStrings(self, n: int) -> int:
        dp = [[i for i in range(5,0,-1)] for _ in range(n)]   # intialize dp matrix
        
        for i in range(1,n):
            for j in range(3,-1,-1):
                dp[i][j] = dp[i - 1][j] + dp[i][j + 1]   # dp expression
                
        return dp[n-1][0]

```

### 🏃 studying with...
#99클럽 #코딩테스트 준비 #개발자 취업 #항해99 #TIL
![til_thumbnail](./img/thmb_python.png)