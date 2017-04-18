---
layout: post
title: Random walk simulate with R - prototype
excerpt: "Making prototype of simulator with R language"
categories: [Math]
comments: true
---

## Random walk simulate with R

Random walk란 무작위 행보라고도 하며 다양한 분야에서 임의의 방향으로 향하는 연속적인 걸음을 나타내는 수학적 개념이다.

### 정의

무작위 행보의 가장 단순한 형태는 다음과 같은 규칙에 의해 생성된 경로이다.

* 시작 점이 있다.
* 경로 상의 한 점에서 다음 점까지의 거리는 상수이다.
* 경로 상의 한 점에서 다음 점으로의 방향은 특정 선호 조건 없이 임의로 선택된다.

때문에, 무작위 행보의 행적은 불규칙하다.

기본적으로 랜덤을 통해 값의 변화를 그래프 등으로 표시하는 것이다.
이걸 구현하기 위해서 R언어를 사용하였다.

먼저 초기값들을 설정한다.
```
# initial price
p0 <- 100

mu <- 0.1
sigma <- 0.2
 ```

변동값을 설정한다.
```
days <- 100
mu.daily <- mu/days
sigma.daily <- sigma * 1/sqrt(days)
```

원하는 개수만큼의 난수를 생성한다.
```
# generate 365 random number
r <- rnorm(365, mu.daily, sigma.daily)
```

난수의 누적합을 구한다.
```
# log(start price) + accumulate total of random number
logPrice <- log(p0) + cumsum(r)
```

자연로그 값이 누적합과 같은 x를 구하여 그래프를 그린다.
```
# exponential distribution of logPrice
Prices <- exp(logPrice)
```

이런식으로 랜덤워크를 구현하고 반복시키면 아래와 같은 그래프가 나온다.

![Random walk graph]({{ site.url }}/img/random-walk-graph.png)

이런 방식으로 랜덤워크를 구현할 수 있지만 현재 단계에서는 여러번 돌렸을 시 하락폭보다는 상승폭이 비교적 많은 것을 볼 수 있다. 컴퓨터는 완전 난수가 아닌 의사 난수를 생성하기 때문에 어쩔 수 없이 나타나는 결과이다.

랜덤워크는 근본적으로 난수가 그래프의 형태와 결과를 거의 결정하는 것이기 때문에 난수 생성에 초점을 두고 다음번엔 여러가지 난수 생성 알고리즘을 통해서 테스트 해볼 계획이다.
