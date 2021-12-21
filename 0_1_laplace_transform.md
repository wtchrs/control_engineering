# Laplace 변환 복습

Laplace 변환은 Fourier 변환과 같이 대표적인 적분 변환(integral transform)이다.
Laplace 변환의 연산자는 $`\mathcal{L}`$ 또는 $`\mathscr{L}`$로 표시한다.
함수 $`f(t)`$의 Laplace 변환 $`F(s)`$는 다음과 같다.

```math
F(s) = \mathscr{L}(f) = \int_{0}^{\infty} e^{-st} f(t) dt
```

## Laplace 변환의 선형성

적분은 선형연산이기 때문에 Laplace 변환도 역시 선형연산이다.
즉, Laplace 변환 가능한 함수 $`f`$, $`g`$에 대하여 다음이 성립한다.

```math
\mathscr{L}\{af(t) + bg(t)\} = a\mathscr{L}\{f(t)\} + b\mathscr{L}\{g(t)\}
```

**증명**)

```math
\mathscr{L}\{af(t) + bg(t)\}
= \int_{0}^{\infty}e^{-st}[af(t) + bg(t)]dt \\
= a \int_{0}^{\infty}e^{-st}f(t)dt + b\int_{0}^{\infty}e^{-st}g(t)dt
= a\mathscr{L}\{f(t)\} + b\mathscr{L}\{g(t)\}
```

## Laplace 변환의 존재성 및 유일성

TODO: Must be added existence and uniqueness theorem of Laplace transform

## s-이동, 제 1 이동정리(First Shifting Theorem)

어떤 수 $`k`$에 대해 $`s>k`$일 때 $`f(t)`$가 변환 $`F(s)`$를 가진다면, $`s-a>k`$에서 $`e^{at}f(t)`$는 변환 $`F(s-a)`$를 가진다.

```math
\mathscr{L}\{e^{at}f(t)\} = F(s-a)
```

또는

```math
e^{at}f(t) = \mathscr{L}^{-1}\{F(s-a)\}
```

**증명**) Laplace 변환의 정의에서 $`s`$를 $`s-a`$로 바꾸면

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

**증명**) Laplace 변환의 정의에 의해 $`e^{-as}F(s)`$는 다음과 같이 나타낼 수 있다.

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

함수 $`f(t)`$의 1계와 2계 도함수의 변환은 다음과 같다.

```math
\mathscr{L} (f') = s\mathscr{L}(f) - f(0) \\
\mathscr{L} (f'') = s^2\mathscr{L}(f) - sf(0) - f'(0)
```

**증명**) $`f'`$이 연속이라면 부분적분에 의해

```math
\begin{aligned}
\mathscr{L}(f') &= \int_0^{\infty}e^{-st}f'(t)dt
= [e^{-st}f(t)] \; \bigg|_0^{\infty}
+ s \int_0^{\infty}e^{-st}f(t)dt \\
&= s \mathscr{L}(f) - f(0)
\end{aligned}
```

TODO

## 참고문헌

- Kreyszig 공업수학 개정 10판(Erwin Kreyszig 저)
