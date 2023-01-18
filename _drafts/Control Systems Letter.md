---
layout: single
title:  "Linear Parameter Varying System"
tags: [Modeling]
comments: true
author_profile: false
toc: true
---



##### IEEE Control Systems Letter (CDC 2023 option) 

###### Introduction 

- Modeling
- Koopman operator
- MPC, LQR

- LPV 

***Notations***
- $||x||^{2}_{W} = x^\top W x$
- $\mathbf{0}_{n\times m}$ : $n \times m$ zero matrix
- Two sets : $\mathbb{X},\mathbb{Y} \subset \mathbb{R}^n$
- $\mathbb{X} \oplus \mathbb{Y}$ : Minkowski sum 
- $\mathbb{X} \ominus \mathbb{Y}$ : Pontryagin set difference  
- Conv$\{\cdot\}$ : Convex hull formed by the vertices of $\{\cdot\}$. 
- $(\cdot)_{k|t}$ : Value at time $t+k$ which is predicted at time $t$. 


###### Koopman operator

***LPV model***
Known B matrix 
Discrete
Full-state measurable system.
$$
\mathbf{x}_{k+1} = \mathbf{A}(\mathbf{p}_k)\mathbf{x}_{k}  + \mathbf{B}\mathbf{u}_{k} 
$$

$$ 
\mathbf{x} \in \mathbb{R}^n, 
\mathbf{u} \in \mathbb{R}^m, \mathbf{p} \in \mathbb{R} \\
\mathbf{A}(\mathbf{p}_k) \in \mathbb{R}^{n\times n},
\mathbf{B} \in \mathbb{R}^{n\times m} \\
$$ 


###### eDMDc for LPV system

M 개의 데이터:

$$
\mathbf{X} = 
\begin{bmatrix}
| & | &  & | \\
\mathbf{x}_1 & \mathbf{x}_2 & \ldots & \mathbf{x}_{M-1} \\
| & | &  & | \\
\end{bmatrix}  \in \mathbb{R}^{n \times (M-1)}
$$

$$
\mathbf{X}^+ = 
\begin{bmatrix}
| & | &  & | \\
\mathbf{x}_2 & \mathbf{x}_3 & \ldots & \mathbf{x}_{M} \\
| & | &  & | \\
\end{bmatrix} \in \mathbb{R}^{n \times (M-1)}
$$

$$
\mathbf{U}_c = 
\begin{bmatrix}
| & | &  & | \\
\mathbf{u}_1 & \mathbf{u}_2 & \ldots & \mathbf{u}_{M-1} \\
| & | &  & | \\
\end{bmatrix}  \in \mathbb{R}^{m \times (M-1)}
$$

$$
\mathbf{X}_p = 
\begin{bmatrix}
| & | &  & | \\
\mathbf{X}_1 \mathbf{p}_1 & \mathbf{X}_2 \mathbf{p}_2 & \ldots & \mathbf{X}_{M-1} \mathbf{p}_{M-1} \\
| & | &  & | \\
\end{bmatrix}  \in \mathbb{R}^{(M-1)}
$$

> $$ \mathbf{X}^+\approx \mathbf{A}\mathbf{X} + \mathbf{A}_p\mathbf{X}_p + \mathbf{B}\mathbf{U_c} $$
>
> **Assumption : known $\mathbf{B}$**
>
> $$ \underbrace{\mathbf{X}^+ - \mathbf{B}\mathbf{U_c}}_{\text{"known"}} \approx \mathbf{A}\mathbf{X} + \mathbf{A}_p\mathbf{X}_p  $$

$$ 
\mathbf{X}^+  - \mathbf{B}\mathbf{U_c}
\approx 
\mathbf{G} \mathbf{\Omega} = \begin{bmatrix}
\mathbf{A} & \mathbf{A}_p \end{bmatrix}
\begin{bmatrix}
\mathbf{X} \\ \mathbf{X}_p
\end{bmatrix}
$$


$$ 
\begin{bmatrix}
\mathbf{A} & \mathbf{A}_p
\end{bmatrix} = 
(\mathbf{X}^+  - \mathbf{B}\mathbf{U_c}) \begin{bmatrix}
\mathbf{X} \\ \mathbf{X}_p
\end{bmatrix}^\dagger
$$



Least square problem : 

$$
||(\mathbf{X}^+  - \mathbf{B}\mathbf{U_c})- \mathbf{G}\mathbf{\Omega}||_F
$$

&rarr; SVD 로 pseudoinverse 찾기

$$
\mathbf{\Omega} = \mathbf{U}\mathbf{\Sigma}\mathbf{V}^* \approx \tilde{\mathbf{U}} \tilde{\mathbf{\Sigma}}\tilde{\mathbf{V}}^* 
$$

그러면 SVD를 통하여 다음과 같이 $\mathbf{G}$를 근사화 할 수 있음

$$
\mathbf{G}\approx \mathbf{\bar{G}} = \mathbf{X}^+
\tilde{\mathbf{V}} \tilde{\mathbf{\Sigma}}^{-1} \tilde{\mathbf{U}}^*
$$

> $$\mathbf{G} \in \mathbb{R}^{n\times (n+m)} $$

$$
\begin{bmatrix}
\mathbf{A} & \mathbf{A}_p
\end{bmatrix}
\approx
\begin{bmatrix}
\mathbf{X}^+
\tilde{\mathbf{V}} \tilde{\mathbf{\Sigma}}^{-1} \tilde{\mathbf{U}}^*_1
& 
\mathbf{X}^+
\tilde{\mathbf{V}} \tilde{\mathbf{\Sigma}}^{-1} \tilde{\mathbf{U}}^*_2
\end{bmatrix}
$$

> $$\tilde{\mathbf{U}}_1 \in \mathbb{R}^{n\times p} $$
> 
> $$\tilde{\mathbf{U}}_2 \in \mathbb{R}^{l\times p} $$


###### Synthesize optimal control

MPC vs NMPC 


$$
\begin{aligned} 
    \min_{\mathbf{z}_{(\cdot)},{\mathbf{\bar{u}}}_{(\cdot)}} \sum_{k=0}^{N-1}  l(&\mathbf{z}_k,\mathbf{\bar{u}}_k)+l_f(\mathbf{z}_N),   \\ 
    \text{s.t. } 
    \mathbf{z}_{k+1} &= A\mathbf{z}_k + B\mathbf{\bar{u}}_k   \\
    \mathbf{z}_k &\in \mathbb{X}   \\
    \mathbf{\bar{u}}_k &\in \mathbb{U}  \\
    \mathbf{z}_N &\in \mathbb{X}_f
\end{aligned}
$$
where $N$ is the prediction horizon, $\mathbb S$ is the RPI set of the system \eqref{pre:error}, $l(\mathbf{z}_k,\mathbf{\bar{u}}_k)$ is the stage cost, $l_f(\mathbf{z}_N)$ is the terminal cost, and $\mathbb{X}_f$ is the terminal constraints.



###### Simulations 

Local linearizatoin
Koopman - LTI
Koopman - LPV (proposed)
비교

lifting function dimension : N 에 따른 비교 
Koopman vs Proposed N에 따른 오차 분포 각 N에 대하여 다른 intitial state, center point of RBF 


###### Discussion

###### References




> Definition 1. RPI set of the LPV system
>> A set $\Omega \subset \mathbb{R}^n$ is a robust invariant set (RPI) set of the LPV system $x^+ = A(p)x + w$, if $A(p)x+w \in \Omega $ for all $x \in \Omega$, $p \in \mathbb{P}$, and $w\in \mathbb{W}$.
