---
layout: single
title: "[알고리즘]소수 만들기"
categories: Algorithm
tags: Algorithm CodingTest
toc: true
author_profile: false
sidebar:
    nav: "docs"
---

# 문제

### **문제 설명**

주어진 숫자 중 3개의 수를 더했을 때 소수가 되는 경우의 개수를 구하려고 합니다. 숫자들이 들어있는 배열 nums가 매개변수로 주어질 때, nums에 있는 숫자들 중 서로 다른 3개를 골라 더했을 때 소수가 되는 경우의 개수를 return 하도록 solution 함수를 완성해주세요.

### 제한사항

- nums에 들어있는 숫자의 개수는 3개 이상 50개 이하입니다.
- nums의 각 원소는 1 이상 1,000 이하의 자연수이며, 중복된 숫자가 들어있지 않습니다.

### 입출력 예

| nums | result |
| --- | --- |
| [1,2,3,4] | 1 |
| [1,2,7,6,4] | 4 |

### 입출력 예 설명

입출력 예 #1

[1,2,4]를 이용해서 7을 만들 수 있습니다.

입출력 예 #2

[1,2,4]를 이용해서 7을 만들 수 있습니다.

[1,4,6]을 이용해서 11을 만들 수 있습니다.

[2,4,7]을 이용해서 13을 만들 수 있습니다.

[4,6,7]을 이용해서 17을 만들 수 있습니다.

# 풀이

```java
class Solution {
	public int solution(int[] nums) {    
		int answer = 0;
		for(int i = 0; i < nums.length; i++) {
		    for(int j = i + 1; j < nums.length; j++) {
		        for(int k = j + 1; k < nums.length; k++) {
		            int num = nums[i] + nums[j] + nums[k];
		            int cnt = 0;
		            for(int m = 2; m < num; m++) {
		                if(num % m == 0)
		                    break;
		                else
		                    cnt++;
		            }
		            if(num - 2 == cnt)
		                    answer++;
				    }
				}
		}

    return answer;
	}
}
```

내가 푼 풀이 방법이다.

위의 문제를 해결하기 위해서 크게 두 가지를 생각했다.

1. nums 배열에서 서로 다른 3개의 수를 어떻게 가져올 것인가.
2. 소수를 어떻게 판별할 것인가.

## 1 . nums 배열에서 서로 다른 3개의 수를 어떻게 가져올 것인가.

```java
for(int i = 0; i < nums.length; i++) {
		    for(int j = i + 1; j < nums.length; j++) {
		        for(int k = j + 1; k < nums.length; k++) {
```

for문 3개를 사용했다.

위의 코드를 사용하면 i, j, k 변수가 반복문을 돌면서 숫자 3개의 배열 인덱스를 가져오는 모든 경우를 다룰 수 있다.

## 2 . 소수를 어떻게 판별할 것인가.

```java
	
	int num = nums[i] + nums[j] + nums[k];
	int cnt = 0;
	for(int m = 2; m < num; m++) {
		if(num % m == 0)
			break;
		else
			cnt++;
	}
	if(num - 2 == cnt)
		answer++;
```

소수는 약수가 1과 자기 자신인 수이다.

num을 1과 num사이의 수로 나눴을 때, 하나라도 나누어 떨어지면 소수가 아니고, **모든 수가 나누어 떨어지지 않아야 소수**이다.

cnt는 나누어 떨어지지 않는 횟수를 세기 위한 변수이다.

num이 소수라면 cnt와 (num - 2)가 같아진다.

소수를 검사할 때 1과 자기자신은 모든 수의 약수이기 때문에 -2를 해주었다.

예를 들어, 7이라는 수는 소수이다. 이를 알기 위해 우리는 7을 1 ~ 7 사이의 수들을 나누었을 때 나누어 떨어지지 않는다. 1과 7을 제외하고 2, 3, 4, 5, 6 총 5개의 수가 나누어 떨어지지 않는다. 

ex) num - 2 == cnt → 7 - 2 = 5

# 정리

내가 짠 코드는 for 반복문이 3번이나 쓰인다.

시간 복잡도가 O(n^3)나 된다는 말이다.

하지만, 혼자 고민도 하고 열심히 찾아본 결과 어쩔 수 없이 위의 코드를 짜야 할 것 같다.

(배열에서 중복 없이 숫자 3개를 꺼내오는 좋은 방법이 있을까....)

소수를 판별하는 더 좋은 방법이 있을 것 같아서 문제를 풀고 나서 찾아봤다.

- 2부터 num 의 제곱근의 정수부분까지만 검사하는 방법
- 에라토스테네스의 체를 이용하는 방법

이렇게 두 가지 방법이 더 있다.   

첫 번째 방법은 내가 풀이한 방법에서 수정할 수 있는 방향이 있다.   

두 번째 방법인 에라토스테네스의 체를 이용하는 것은 위의 문제를 풀이하는 데에 조금 어려움이 있다.   

왜냐하면 에라토스테네스는 소수인 수의 배수들을 지워나가면서 소수를 찾는 방법인데 위의 문제는 주어진 수가 소수인가를 판별하는 문제이기 때문에 문제를 해결하는 방향에 있어 두 개가 다르다고 생각한다.

