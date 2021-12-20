# Laplace 변환 복습

Laplace 변환은 Fourier 변환과 같이 대표적인 적분 변환(integral transform)이다.
Laplace 변환의 연산자는 $\mathcal{L}$ 또는 $\mathscr{L}$로 표시한다.
함수 $f(t)$의 Laplace 변환 $F(s)$는 다음과 같다.

$$
F(s) = \mathcal{L}(f) = \int_{0}^{\infty} e^{-st} f(t) dt
$$

## Laplace 변환의 선형성

적분은 선형연산이기 때문에 Laplace 변환도 역시 선형연산이다.
즉, Laplace 변환 가능한 함수 $f$, $g$에 대하여 다음이 성립한다.

$$
\mathcal{L}\{af(t) + bg(t)\} = a\mathcal{L}\{f(t)\} + b\mathcal{L}\{g(t)\}
$$

증명)

$$
\mathcal{L}\{af(t) + bg(t)\}
= \int_{0}^{\infty}e^{-st}[af(t) + bg(t)]dt \\
= a \int_{0}^{\infty}e^{-st}f(t)dt + b\int_{0}^{\infty}e^{-st}g(t)dt
= a\mathcal{L}\{f(t)\} + b\mathcal{L}\{g(t)\}
$$

## s-이동, 제 1 이동정리(First Shifting Theorem)

$f(t)$가 변환 $F(s)$를 가진다면, $s>a$에서 $e^{at}f(t)$는 변환 $F(s-a)$를 가진다.

$$
\mathcal{L}\{e^{at}f(t)\} = F(s-a)
$$

또는

$$
e^{at}f(t) = \mathcal{L}^{-1}\{F(s-a)\}
$$

증명)

$$
F(s-a) = \int_0^{\infty} e^{-(s-a)t}f(t)dt = \int_0^{\infty} e^{-st} e^{at}f(t)dt = \mathcal{L}\{e^{at}f(t)\}
$$

## t-이동(시간이동), 제 2 이동정리(Second Shifting Theorem)

먼저 단위계단함수(unit step function)를 정의한다.
단위계단함수 $u(t)$, 또는 임의의 상수 $a$에 대하여 $u(t-a)$는 다음과 같이 정의한다.

$$
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
$$

$f(t)$의 변환 $F(s)$가 존재한다면 다음과 같은 이동함수(shifted function)
$$
\begin{aligned}
\tilde f(t) = f(t-a)u(t-a) =
\begin{cases}
0, & if \; t < a \\
f(t-a) \quad & if \; t > a
\end{cases}
\end{aligned}
$$
의 변환은 다음과 같다.
$$
\mathcal{L} \{f(t-a)u(t-a)\} = e^{-as}F(s)
$$

## 참고문헌

- Kreyszig 공업수학 개정 10판(Erwin Kreyszig 저)
