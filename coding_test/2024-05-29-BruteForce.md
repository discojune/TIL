# 99클럽 코테 스터디 10일차 TIL : Brute Force(완전 탐색)

## 소수 찾기
프로그래머스 문제 링크:
- https://school.programmers.co.kr/learn/courses/30/lessons/42839


## 풀이 1. 완전 탐색

### 🤔 시행 착오
종이 조각으로 만들 수 있는 숫자를 계산하는 간단한 방법이 떠오르지 않아, 종이 조각으로 만들 수 있는 가장 큰 수 이하의 모든 소수를 구하는 방법을 사용했다.

종이 조각으로 만들 수 있는 가장 큰 수 이하의 모든 소수에서 다음의 조건을 통해 불만족하는 소수를 제외하고 만족하는 소수의 개수를 반환하는 방법으로 문제를 풀었다.

1. 종이 조각의 최대 수 이하의 모든 수를 구한다.
2. 종이 조각을 일부 혹은 전체 사용한 경우, 즉 초과해서 사용한 경우를 제외한다.
3. 종이 조각 외 숫자가 포함된 경우를 제외한다.
4. 위의 조건을 만족한 수가 소수인지 판별한다.

하지만 이 알고리즘으로 한 문제에서 시간 초과가 발생했다.

이 알고리즘은 다음의 부분에서 시간복잡도가 커지는 문제가 있었다.

1. 종이 조각의 최대 수 이하의 모든 수를 대상으로 하는 부분
2. 종이 조각으로 구할 수 있는 최대 값을 X라고 했을 때 소수를 구하는 부분에서 2부터 X의 제곱근까지의 모든 수를 for문으로 반복하며 X가 해당 수로 나눠떨어지면 소수가 아니므로 제외하는 부분


### 💡 새롭게 알게 된 것
소수를 구하는 방법에서 거의 선형에 가깝게 풀 수 있는 법을 [참조](https://velog.io/@changhee09/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EC%86%8C%EC%88%98%EC%9D%98-%ED%8C%90%EB%B3%84-%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98-%EC%B2%B4) (에라토스테네스의 체 항목 참고)하였다.

또한 기존의 알고리즘을 다음과 같이 변경하여 모든 문제를 통과할 수 있었다.

1. 에라토스테네스의 체로 종이 조각의 최대 수 이하의 소수를 먼저 구한다.
2. 종이 조각을 일부 혹은 전체 사용한 경우, 즉 초과해서 사용한 경우를 제외한다.
3. 종이 조각 외 숫자가 포함된 경우를 제외한다.

### 🎉 풀이 코드
```python
def solution(numbers):
    from collections import Counter
    from math import sqrt

    
    answer = 0
    
    numbers_c = Counter(numbers)

    # 종이 조각으로 만들 수 있는 가장 큰 수
    max_number = int(''.join(sorted(numbers, reverse=True)))
    
    # 소수를 구하는 "에라토스테네스의 체" 알고리즘 적용
    prime_num_check = [True for _ in range(max_number + 1)]
    
    for i in range(2, int(sqrt(max_number))+1):
        if prime_num_check[i]:
            
            prime_num = 2
            
            while i * prime_num <= max_number:
                prime_num_check[i * prime_num] = False
                
                prime_num += 1

    # 종이 조각으로 만들 수 있는 최대 수 이하의 모든 소수   
    prime_numbers = [] 
    
    for i in range(2, max_number + 1):
        if prime_num_check[i]:
            prime_numbers.append(i)
            
    
    # 소소 중에 종이 조각으로 만들 수 있는 소수를 찾는 알고리즘
    for num in prime_numbers:
        num_c = Counter(str(num))
        is_valid = True

        for n in num_c:
            # 제공된 종이 조각보다 더 많은 조각를 사용한 경우
            if num_c[n] > numbers_c[n]:
                is_valid = False
                break

            # 제공된 종이 조각 외의 숫자가 포함된 경우
            if n not in numbers:
                is_valid = False
                break
                    
        if is_valid:
            answer += 1
        
    return answer

```

### 🏃 studying with...
#99클럽 #코딩테스트 준비 #개발자 취업 #항해99 #TIL
![til_thumbnail](./img/thmb_python.png)