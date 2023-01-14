---
layout: single
title:  "Koopman Operator"
tags: [Koopman Operator, All]
comments: true
author_profile: false
toc: true
---


## What is Koopman Operator ?

Koopman Operator는 비선형 시스템을 (by evolving functions of the state "as known as observable function") infinite-dim.의 선형 시스템으로 표현해주는 Operator.

(In application) infinite-dim.으로 표현하는 것은 어렵기 때문에 finite-dim.의 선형 시스템으로 근사화하여 표현함.

![title](/fig/koopman_concept.png){: width="600"}{: .align-center}

How to approximate
- Data-driven
- <mark>No prior information</mark>
- DMD, EDMD, NN 등의 방법들이 사용됨

## Basic Mathematical Formulation

Discrete-time 시스템:

$$
x_{k+1} = f(x_k)
$$

where $x_k \in \mathbb{R}^x$.

Let observation function: $g(x) \in \mathbb{G} : \mathbb{R}^x \rightarrow \mathbb{R}^y$.

$$
y_k = g(x_k)
$$

where $y_k \in \mathbb{R}^y$.

Let Koopman operator $\mathcal K : \mathbb{G} \rightarrow \mathbb{G}$.

$$
  \mathcal{K}g (x) = g(f(x))
$$

{: .notice--info}
$$
  \mathcal{K}g (x_k) = g(f(x_k)) = g(x_{k+1})
$$

{: .notice--info}
&rarr; Koopman operator 를 이용하여 $y$ 를 propagate 하는 것과 propagate한 $x$를 $y$로 lift 한것이 같음.

## Approximating a Koopman Operator
Let user-defined vector-valued function $\Psi(x)$ as follwos:

$$
\Psi(x) = [\psi_1 (x), \psi_2 (x), \ldots, \psi_N (x)].
$$

이 함수들로 다음과 같이 $y_k = g(x_k)$를 다시 표현할 수 있음

$$
y_k = \Psi(x_k)
$$

그러면 Koopman operator는 다음의 관계를 가짐

$$
\Psi(x_{k+1}) = K\Psi(x_k) + w
$$

where $K\in \mathbb{C}^{N\times N}$ and w is an error.

$$
\text{Cost function} : J = \sum^{P-1}_{p=1} || \Psi(x_{p+1}) - K\Psi(x_{p}) ||^2
$$


P : 데이터 개수

$J$를 최소화 하는 $K$ 찾아야함 (by Least-square, NN 등등)
```
NN를 사용하는 경우, user-defined vector-valued function을 네트워크로 찾을 수 있음.
```


Least-square를 사용하는 경우에 다음의 방식으로 간단히 계싼가능.

$$
K = G^\dagger A,\\
G = ,\\
A = \frac{1}{P} 
$$

<!-- ``` 
search: false
$$
\begin{bmatrix}
x_2\\
y_2\\
z_2  
\end{bmatrix}
= R \begin{bmatrix}
                  x_1\\
                  y_1\\
                  z_1  
                  \end{bmatrix}
$$
```

**Note:** `search: false` only works to exclude posts when using **Lunr** as a search provider. \overline{bel}(x_t) = \int_{x_{t-1}}p(x_t \mid x_{t-1}, u_{t}) bel(x_{t-1}) dx_{t-1}

{: .notice--info}

To exclude files when using **Algolia** as a search provider add an array to `algolia.files_to_exclude` in your `_config.yml`. For more configuration options be sure to check their [full documentation](https://community.algolia.com/jekyll-algolia/options.html).
$$
\overline{bel}(x_t) = \int_{x_{t-1}}p(x_t \mid x_{t-1}, u_{t}) bel(x_{t-1}) dx_{t-1}
$$


```yaml
algolia:
  # Exclude more files from indexing
  files_to_exclude:
    - index.html
    - index.md
    - excluded-file.html
    - _posts/2017-11-28-post-exclude-search.md
    - subdirectory/*.html
``` -->



## References
[1] Ian Abraham et al., "[Model-Based Control Using Koopman Operators](https://arxiv.org/pdf/1709.01568.pdf)", RSS 2017

[2] Ian Abraham et al., "[Active Learning of Dynamics for Data-Driven Control Using Koopman Operators](https://ieeexplore.ieee.org/abstract/document/8759089)", TRO 2019