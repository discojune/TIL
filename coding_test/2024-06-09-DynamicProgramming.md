# 99클럽 코테 스터디 21일차 TIL : 동적계획법(Dynamic Programming)

## Count Square Submatrices with All Ones
리트코드 문제 링크:
- https://leetcode.com/problems/count-square-submatrices-with-all-ones/description/


## 풀이 1. 동적계획법

### 🤔 시행 착오
오늘의 문제 풀이는 예제는 통과했지만 시간 초과로 인해 통과가 되지 못했다.

numpy를 사용하여 NxN의 슬라이딩 윈도우로 합이 N*N이 되는 경우 이전 단계의 사각형의 갯수 dp[n-1] + dp[n]을 더하면서 최종 값을 구하는 방법으로 문제를 풀었다.

### 😅 개선이 필요한 풀이 코드
```python
class Solution:
    def countSquares(self, matrix: List[List[int]]) -> int:
        import numpy as np

        m, n = len(matrix), len(matrix[0])
        max_size = min(m, n)

        dp = [0] * max_size

        matrix = np.array(matrix)

        for s in range(1, max_size+1):
            if s == 1:
                dp[s-1] = np.sum(matrix)
                continue

            squares = 0
            for i_m in range(0, m - (s-1)):
                for i_n in range(0, n - (s-1)):
                    square = matrix[i_m : i_m + s, i_n : i_n + s]
                    if np.sum(square) == s*s:
                        squares += 1

            dp[s-1] = squares + dp[s-2]

        return dp[-1]

```

### 💡 새롭게 알게 된 것
이 문제의 핵심은 (i, j) 위치에서 끝나는 사각형의 최대 크기를 저장하는 dp를 만들고 값을 저장해나가는 것이다.
이때 인접한 사각형을 구하기 위해 
```matrix[i][j]```가 1인 경우 ```dp[i][j] = min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + 1```를 통해 값을 업데이트해 나간다.

#### Table
| Index (i, j) | matrix | dp      | Reason                                                 |
|--------------|--------|---------|--------------------------------------------------------|
| (0, 0)       | 0      | 0       | matrix[0][0] is 0, so dp[0][0] is 0                    |
| (0, 1)       | 1      | 1       | matrix[0][1] is 1, so dp[0][1] is 1                    |
| (0, 2)       | 1      | 1       | matrix[0][2] is 1, so dp[0][2] is 1                    |
| (0, 3)       | 1      | 1       | matrix[0][3] is 1, so dp[0][3] is 1                    |
| (1, 0)       | 1      | 1       | matrix[1][0] is 1, so dp[1][0] is 1                    |
| (1, 1)       | 1      | 1       | matrix[1][1] is 1, so dp[1][1] is 1 + min(1,1,0) = 1   |
| (1, 2)       | 1      | 2       | matrix[1][2] is 1, so dp[1][2] is 1 + min(1,1,1) = 2   |
| (1, 3)       | 1      | 2       | matrix[1][3] is 1, so dp[1][3] is 1 + min(1,2,1) = 2   |
| (2, 0)       | 0      | 0       | matrix[2][0] is 0, so dp[2][0] is 0                    |
| (2, 1)       | 1      | 1       | matrix[2][1] is 1, so dp[2][1] is 1 + min(1,0,1) = 1   |
| (2, 2)       | 1      | 2       | matrix[2][2] is 1, so dp[2][2] is 1 + min(2,1,1) = 2   |
| (2, 3)       | 1      | 3       | matrix[2][3] is 1, so dp[2][3] is 1 + min(2,2,2) = 3   |

Total number of squares = 15


### 📚 참고 풀이 코드
```python
class Solution(object):
    def countSquares(self, matrix):
        m, n = len(matrix), len(matrix[0])
        dp = [[0] * (n+1) for _ in range(m+1)] # new int[m+1][n+1];
        ans = 0
        for i in range(m):
            for j in range(n):
                if matrix[i][j]:
                    dp[i][j] = min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + 1
                    ans += dp[i][j]
        return ans

```

### 🏃 studying with...
#99클럽 #코딩테스트 준비 #개발자 취업 #항해99 #TIL
![til_thumbnail](./img/thmb_python.png)