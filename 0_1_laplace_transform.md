# Laplace 변환 복습

Laplace 변환은 Fourier 변환과 같이 대표적인 적분 변환(integral transform)이다.
Laplace 변환의 연산자는 $`\mathcal{L}`$ 또는 $`\mathscr{L}`$로 표시한다.
함수 $`f(t)`$의 Laplace 변환 $`F(s)`$는 다음과 같다.

```math
F(s) = \mathscr{L}(f) = \int_{0}^{\infty} e^{-st} f(t) dt
```

## Laplace 변환의 선형성(Linearity)

적분은 선형연산이기 때문에 Laplace 변환도 역시 선형연산이다.
즉, Laplace 변환 가능한 함수 $`f`$, $`g`$에 대하여 다음이 성립한다.

```math
\mathscr{L}\{af(t) + bg(t)\} = a\mathscr{L}\{f(t)\} + b\mathscr{L}\{g(t)\}
```

##### 증명)

```math
\mathscr{L}\{af(t) + bg(t)\}
= \int_{0}^{\infty}e^{-st}[af(t) + bg(t)]dt \\
= a \int_{0}^{\infty}e^{-st}f(t)dt + b\int_{0}^{\infty}e^{-st}g(t)dt
= a\mathscr{L}\{f(t)\} + b\mathscr{L}\{g(t)\}
```

## Laplace 변환의 존재성(Existence) 및 유일성(Uniqueness)

#### Laplace 변환의 존재정리

반축(semi-axis) $`t \geq 0`$ 상에서 조각적 연속인 함수 $`f(t)`$가 모든
$`t \geq 0`$와 어떤 상수 $`M`$과 $`k`$에 대해서 다음의 '증가제한(growth restriction)'

```math
|f(t)| \leq Me^{kt}
```

을 만족하면, 모든 $`s>k`$에 대해 $`f(t)`$의 Laplace 변환 $`\mathscr{L}(f)`$가 존재한다.

##### 증명)

$`f(t)`$가 조각적 연속이고, $`s>k`$이므로

```math
\begin{aligned}
| \mathscr{L}(f) |
&= \left| \int_0^{\infty} e^{-st}f(t)dt \right|
\leq \int_0^{\infty} e^{-st} |f(t)| dt \\
&\leq \int_0^{\infty} Me^{kt} e^{-st} dt
= \int_0^{\infty} Me^{(k - s)t} dt
= {M \over s - k}
\end{aligned}
```

여기서 $`s > k`$가 아니면 마지막 적분이 존재하지 않기 때문에, $`s > k`$의 조건이 있어야 존재성을 보장할 수 있다. [^1]

**TODO**: need to add content about uniqueness of Laplace transform.

## s-이동, 제 1 이동정리(First Shifting Theorem)

어떤 수 $`k`$에 대해 $`s>k`$일 때 $`f(t)`$가 변환 $`F(s)`$를 가진다면, $`s-a>k`$에서 $`e^{at}f(t)`$는 변환 $`F(s-a)`$를 가진다.

```math
\mathscr{L}\{e^{at}f(t)\} = F(s-a)
```

또는

```math
e^{at}f(t) = \mathscr{L}^{-1}\{F(s-a)\}
```

##### 증명)

Laplace 변환의 정의에서 $`s`$를 $`s-a`$로 바꾸면

```math
F(s-a) = \int_0^{\infty} e^{-(s-a)t}f(t)dt = \int_0^{\infty} e^{-st} e^{at}f(t)dt = \mathscr{L}\{e^{at}f(t)\}
```

만약 $`s-a>k`$이면, 가정에 의해 위 적분이 존재한다.

## t-이동(시간이동), 제 2 이동정리(Second Shifting Theorem)

먼저 단위계단함수(unit step function)를 정의한다.
단위계단함수 $`u(t)`$, 또는 임의의 상수 $`a`$에 대하여 $`u(t-a)`$는 다음과 같이 정의한다.

```math
\begin{aligned}
u(t) = &
\begin{cases}
0, \quad if \; t < 0 \\
1, \quad if \; t > 0
\end{cases} \\ \\
u(t-a) = &
\begin{cases}
0, \quad if \; t < a \\
1, \quad if \; t > a
\end{cases}
\end{aligned}
```

$`f(t)`$의 변환 $`F(s)`$가 존재한다면 다음과 같은 이동함수(shifted function)

```math
\begin{aligned}
\tilde f(t) = f(t-a)u(t-a) =
\begin{cases}
0, & if \; t < a \\
f(t-a) \quad & if \; t > a
\end{cases}
\end{aligned}
```

의 변환은 다음과 같다.

```math
\mathscr{L}\{\tilde f(t)\} = \mathscr{L} \{f(t-a)u(t-a)\} = e^{-as}F(s)
```

##### 증명)

Laplace 변환의 정의에 의해 $`e^{-as}F(s)`$는 다음과 같이 나타낼 수 있다.

```math
e^{-as}F(s) = e^{-as} \int_0^{\infty}e^{-\tau s}f(\tau)d\tau
= \int_0^{\infty}e^{-(\tau+a)s}f(\tau)d\tau
```

$`\tau + a = t`$, $`d\tau = dt`$로 치환하면

```math
e^{-as}F(s) = \int_a^{\infty}e^{-st}f(t-a)dt
```

적분구간의 하한이 변한 것에 주의해야 한다. 단위계단함수를 피적분함수에 곱하여 적분구간의 하한을 0으로 바꿀 수 있다.

```math
e^{-as}F(s) = \int_0^{\infty}e^{-st}f(t-a)u(t-a)dt
= \int_0^{\infty}e^{-st} \tilde f(t)dt
```

## 도함수의 Laplace 변환

어떤 함수 $`f`$의 Laplace 변환이 존재할때, $`f(t)`$의 1계와 2계 도함수의 변환은 다음과 같다.

```math
\mathscr{L} (f') = s\mathscr{L}(f) - f(0) \\
\mathscr{L} (f'') = s^2\mathscr{L}(f) - sf(0) - f'(0)
```

##### 증명)

$`f'`$이 연속이라면 부분적분에 의해

```math
\begin{aligned}
\mathscr{L}(f') &= \int_0^{\infty}e^{-st}f'(t)dt
= [e^{-st}f(t)] \; \bigg|_0^{\infty}
+ s \int_0^{\infty}e^{-st}f(t)dt \\
&= s \mathscr{L}(f) - f(0)
\end{aligned}
```

$`f'`$이 조각적 연속일 때에도 동일하게 증명 가능하다.

2계 도함수에 대한 Laplace 변환은 1계 도함수의 Laplace 변환을 먼저 적용한 뒤
1계 도함수의 Laplace 변환을 대입하여 얻을 수 있다.

```math
\mathscr{L}(f'') = s \mathscr{L}(f') - f'(0)
= s[s \mathscr{L}(f) - f(0)] - f'(0)
= s^2 \mathscr{L}(f) - sf(0) - f'(0)
```

귀납법을 사용하여 다음 정리를 얻을 수 있다.

#### 임의 계수의 도함수 $`f^{(n)}`$의 Laplace 변환

$`f`$, $`f'`$, $`\dots`$, $`f^{(n-1)}`$이 반축 $`t \geq 0`$ 위의 모든 부분공간에서 조각적 연속이고
[존재정리](#laplace-변환의-존재정리)에서의 증가제한 조건을 만족할 때
$`f^{(n)}`$이 반축 $`t \geq 0`$ 위의 모든 유한구간에서 조각적 연속이면 $`f^{(n)}`$의 변환은

```math
\mathscr{L}(f^{(n)})
= s^n\mathscr{L}(f) - s^{n-1}f(0) - s^{n-2}f'(0) - \dots - f^{(n-1)}(0)
```

이다.

## 함수의 적분의 Laplace 변환

**TODO**

## 참고문헌

- Kreyszig 공업수학 개정 10판(Erwin Kreyszig 저)

[^1]: [엄밀한 증명][ref-existence]

[ref-existence]: https://freshrimpsushi.github.io/posts/definition-of-laplace-transform-and-proof-of-existence-of-laplace-transform/
