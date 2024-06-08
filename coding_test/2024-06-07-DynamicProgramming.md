# 99클럽 코테 스터디 20일차 TIL : 동적계획법(Dynamic Programming)

## Partition Array for Maximum Sum
리트코드 문제 링크:
- https://leetcode.com/problems/partition-array-for-maximum-sum/description/


## 풀이 1. 동적계획법

### 🤔 시행 착오
오늘 문제는 문제를 이해하기 어려웠고, 어설프게 tabulation 방식을 사용해봤지만 해답을 보고나니 전혀 틀린 방향이었다.
discussion이나 다른 블로그를 참고해도 해답을 이해하기 어려워서 ChatGPT의 도움을 빌렸다.

풀이와 중간 과정을 테이블로 풀어보니 이해가 되었다.

#### Table
| Index (i) | dp[i] | Reason                                 |
|-----------|-------|----------------------------------------|
| 0         | 1     | max([1]) * 1 = 1                       |
| 1         | 30    | max([15]) * 1 + dp[0] = 15             |
|           |       | max([1, 15]) * 2 = 30                  |
| 2         | 45    | max([7]) * 1 + dp[1] = 37              |
|           |       | max([15, 7]) * 2 + dp[0] = 31          |
|           |       | max([1, 15, 7]) * 3 = 45               |
| 3         | 54    | max([9]) * 1 + dp[2] = 54              |
|           |       | max([7, 9]) * 2 + dp[1] = 48           |
|           |       | max([15, 7, 9]) * 3 + dp[0] = 46       |
| 4         | 63    | max([2]) * 1 + dp[3] = 56              |
|           |       | max([9, 2]) * 2 + dp[2] = 63           |
|           |       | max([7, 9, 2]) * 3 + dp[1] = 57        |
| 5         | 72    | max([5]) * 1 + dp[4] = 68              |
|           |       | max([2, 5]) * 2 + dp[3] = 64           |
|           |       | max([9, 2, 5]) * 3 + dp[2] = 72        |
| 6         | 84    | max([10]) * 1 + dp[5] = 82             |
|           |       | max([5, 10]) * 2 + dp[4] = 83          |
|           |       | max([2, 5, 10]) * 3 + dp[3] = 84       |


### 💡 새롭게 알게 된 것
이 문제의 핵심은 주어진 배열의 0번째 값부터 시작하여 1부터 최대 길이가 k인 sub array를 만들고, 

이번 인덱스의 값에서 sub array(1부터 k 길이)와 이전 인덱스인 ```i - j + 1```번째 값까지의 최대 sub array의 값을 더하여 가장 최대값이 되는 조합을 저장해나가는 것이다.

### 📚 참고 풀이 코드
```python
class Solution:
    def maxSumAfterPartitioning(self, arr: List[int], k: int) -> int:
        n = len(arr)
        dp = [0] * n
        
        for i in range(n):
            max_val = 0
            for j in range(1, k+1):
                if i - j + 1 >= 0:
                    max_val = max(max_val, arr[i - j + 1])
                    if i - j >= 0:
                        dp[i] = max(dp[i], dp[i - j] + max_val * j)
                    else:
                        dp[i] = max(dp[i], max_val * j)
        
        return dp[-1]

```

### 🏃 studying with...
#99클럽 #코딩테스트 준비 #개발자 취업 #항해99 #TIL
![til_thumbnail](./img/thmb_python.png)