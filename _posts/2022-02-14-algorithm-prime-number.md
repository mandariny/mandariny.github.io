---
layout: singel
title: "[Algorithm] 소수 판별 / 에라토스테네스의 체"
---

**key word** : 소수, 소수 판별, Prime Number

<br><br>

소수란 1과 자기 자신만을 약수로 가지는 자연수이다. 일반적으로 for문을 통해 판별하려는 수까지의 모든 수로 나눠본다면 쉽게 소수인지 아닌지 판별할 수 있다. 하지만 O(n)의 시간이 소모되어 판별해야하는 수의 양이 많을수록 비효율적이게 된다. 에라토스테네스의 체 알고리즘을 사용한다면 보다 효율적으로 더 많은 양의 소수를 판별할 수 있다.

<br><br>

## 단일 숫자의 소수 판별

가장 기본적으로 `for(int i=2; i < n; i++)`을 통해 소수를 판별할 수 있다. 하지만 이는 O(n)의 시간복잡도를 가지므로 꽤나 비효율적이다.

좀 더 시간을 줄이기 위해서는 확인하는 숫자의 범위를 줄일 필요가 있다.

첫번째로 수의 범위를 절반으로 줄일 수 있다. 자기 자신 이외에는 1/2한 수보다 큰 수를 약수로 가질 수 없기때문이다.

여기에서 한 번 더 범위를 줄일 수 있는데, 바로 제곱근까지의 수만 확인하는 것이다. 두 수의 곱으로 자연수를 나타낼 때에 제곱근을 기준으로 대칭인 수의 쌍이 나타난다. 예를 들어 곱해서 16이 되는 수의 쌍은 (1, 16), (2, 8), (4, 4), (8, 2), (16, 1)로, 제곱근인 (4, 4)를 기준으로 같은 쌍의 수들이 대칭으로 나타난다. 따라서 제곱근까지 확인했을 때 약수가 없다면 그 이상을 확인하지 않아도 그 수가 소수라 판단할 수 있다. 이때의 시간 복잡도는 O(n^1/2)로 O(n)에 비하면 꽤 효율적인 시간 내에 소수를 구할 수 있다.

<br><br>

## 에라토스테네스의 체

에라토스테네스의 체는 특정 범위가 주어지고 범위 내 소수를 모두 찾아야하는 상황에서 사용하기 좋은 알고리즘이다. 범위가 커지면 커질수록 위와 같은 방식으로 숫자를 하나씩 판별하는 것이 비효율적이고 오래 걸린다. 하지만 1이 아닌 어떤 수의 배수는 소수가 아니라는 점을 이용해 O(n log n)의 시간 내에 소수를 판별할 수 있다. 우선 범위에 해당하는 숫자 배열을 만들고, 2이상인 수에 대해 자기 자신을 제외한 배수를 제거한다. 그렇게 제거하고 마지막까지 남은 수들이 소수가 되는 것이다.

<br><br>

## 에라토스테네스의 체 구현

```
public class Main {
	public static void main(String[] args) {
		primeNum(100);
	}

	public static void primeNum(int num) {
		boolean[] check = new boolean[num + 1];

		check[0] = true;
		check[1] = true;

		for(int i=2; i<check.length; i++) {
			for(int j=i * 2; j<check.length; j += i) {
				check[j] = true;
			}
		}

		for(int i=2; i<check.length; i++) {
			if(!check[i])
				System.out.print(i + ", ");
		}
	}
}
```