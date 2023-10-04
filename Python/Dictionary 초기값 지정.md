# Dictionary 초기값 지정

파이썬의 dictionary는 단어 그대로 '사전'이라는 의미로 key-value 한 쌍을 가지는 자료형이다. dictionary는 알고리즘에서 횟수 세기에 유용하게 사용된다. 아래 예제는 sports 리스트에서 각 원소의 등장 횟수를 계산한다. 보통 아래와 같이 dictionary를 이용해서 코드를 짠다. 하지만 원소가 처음 등장할 때 if 조건문을 따로 명시해 줘야 하는데 이는 가독성이 떨어진다.

```python
sports = ["soccer", "baseball", "basketball"]
num_sports = {}
for i in sports:
    if i not in num_sports:
        num_sports[i] = 0
    num_sports[i] += 1
print(num_sports)
```

이처럼 dictionary에 기본값을 설정해줘야 할 때는 파이썬의 내장 모듈인 collections의 defaultdict 클래스를 사용하면 된다. 위 코드를 수정해보자.

```python
from collections import defaultdict

sports = ["soccer", "baseball", "basketball"]
num_sports = defaultdict(int)
for i in sports:
    num_sports[i] += 1
print(num_sports)
```

여기서 num_sports = defaultdict(int)이 기본값 0으로 세팅해주는 코드이다.  
dictionary에서 어떤 key 값이 처음 등장하면 선언 때 받은 입력 defaultdict(int)을 함수로 실행시켜 리턴값을 대입한다. 따라서 int 함수를 실행하게 되는데 파이썬에서 int()는 결과가 0이기 때문에 초기값은 0으로 세팅된다. 

> 관련 문제 : [백준 4358 생태학](https://www.acmicpc.net/problem/4358)
