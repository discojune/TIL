# 99클럽 코테 스터디 23일차 TIL : 이분 탐색(Binary Search)

## Capacity To Ship Packages Within D Days
리트코드 문제 링크:
- https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/description/


## 풀이 1. 이분 탐색

### 🤔 시행 착오
이분 탐색 개념이 아직 익숙하지 않아 예시에 나온 것처럼 무게를 어떻게 묶을지에 초점을 맞추니 문제 해결이 어려웠다.

### 💡 새롭게 알게 된 것
이분 탐색의 핵심은 최소와 최대 조건을 잘 판단하는 것 같다.

제한조건인 일수에 대해서 무게의 가장 최소값을 찾는 문제이므로 무게에 대한 최소, 최대값을 지정하고, 일수와 비교하며 최소, 최대를 조정하는 방법으로 문제를 풀 수 있다.

### 📚 참고 풀이 코드
```python
class Solution:
    def shipWithinDays(self, weights: List[int], days: int) -> int:
        def check(mid):
            capacity = mid
            count_days = 1

            for weight in weights:
                if weight > capacity :
                    if count_days >= days:
                        return True
                    count_days += 1
                    capacity = mid     
                capacity -= weight

            return False

        left = max(weights)
        right = math.ceil(len(weights) / days) * max(weights)

        while left < right:
            mid = (left+right) // 2

            if check(mid):
                left = mid + 1
            else:
                right = mid

        return left

```

### 🏃 studying with...
#99클럽 #코딩테스트 준비 #개발자 취업 #항해99 #TIL
![til_thumbnail](./img/thmb_python.png)