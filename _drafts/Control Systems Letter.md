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


###### Optimal control

###### Simulations 

Local linearizatoin
Koopman - LTI
Koopman - LPV
비교

lifting function dimension : N 에 따른 비교



###### Discussion

###### References







\subsection{Tube-based Model Predictive Control}
\begin{definition} [RPI set of the LTI system]
A set $\Omega \subset \mathbb{R}^n$ is a {\color{blue}robust invariant set (RPI)} set of the LTI system $x^+ = Ax + w$, if $Ax+w \in \Omega $ for all $x \in \Omega$ and $w\in \mathbb{W}$.
\end{definition}

Consider the following LTI system:
\begin{equation} 
\begin{aligned}
\label{eq:actual_system}
    \mathbf{x}_{k+1} = A \mathbf{x}_k &+ B \mathbf{u}_k + \mathbf{w}_k, \\
\text{s.t. }\mathbf{x}_k  &\in \mathbb{X}, \\
                \mathbf{u}_k  &\in \mathbb{U}, 
\end{aligned}
\end{equation}
where $k$ is the time index, and $\mathbf{x}_k \subset \mathbb{R}^n $ and $\mathbf{u}_k \subset \mathbb{R}^m $ are the state and input vectors, respectively. Let $\mathbf{w}_k \in \mathbb W \subset \mathbb{R}^n$ be a bounded disturbance vector. The nominal system {\color{blue}of \eqref{eq:actual_system} (without the disturbance) is given} as follows:
\begin{equation}
\mathbf{z}_{k+1} = A\mathbf{z}_k + B\mathbf{\bar{u}}_k,
\label{eq:nominal_system}
\end{equation}
where $\mathbf{\bar{u}}_k$ is the nominal input that is derived from a nominal MPC and $\mathbf{z}_k$ is the nominal state. Then the control input of the TMPC is {\color{blue}now designed} as follows:
\begin{equation}
 \mathbf{u}_k= \mathbf{\bar{u}}_k + K(\mathbf{x}_k-\mathbf{z}_k),
 \label{eq:TMPC_control}
\end{equation}
where {\color{blue}the second term in \eqref{eq:TMPC_control}} is the auxiliary state feedback control that keeps the actual system in the invariant tube by compensating for the error. 
Let $\mathbf{e}_k = \mathbf{x}_k - \mathbf{z}_k$ be the error vector. Then the error system can be {\color{blue}written} by \eqref{eq:actual_system}-\eqref{eq:TMPC_control} as follows:
\begin{equation}
\label{pre:error}
\begin{aligned} 
\mathbf{e}_{k+1} & = A(\mathbf{x}_k-\mathbf{z}_k) + B(\mathbf{u}_k - \mathbf{\bar{u}}_k) + \mathbf{w}_k 
\\ 
    &  = (A + BK) \mathbf{e}_k + \mathbf{w}_k.
\end{aligned}
\end{equation}
If the system $A + BK $ is Schur stable, then an RPI set $\mathbb{S}$ {\color{blue}of the LTI error system \eqref{pre:error}} can be computed by iterative Minkowski sum, as {\color{blue}done in} \Cref{algorithm:LTI_RPI}.
\begin{algorithm} [b]
\caption{Calculation of an RPI set $\mathbb{S}$ of an LTI system.}\label{alg:cap}
\begin{algorithmic}[1]
\State $\mathbb{E}_0 \leftarrow  \{\mathbf{0}\}$, $\mathbb{E}_1 \leftarrow \mathbb{W}$
\State $k \leftarrow 0$
\While{$\mathbb{E}_{k+1} \nsubseteq \mathbb{E}_{k}$} \label{al:eps} 
    \State $k = k + 1$
    \State $\mathbb{E}_{k+1} = (A+BK)\mathbb{E}_{k} \oplus \mathbb{W}$
\EndWhile
\State $\mathbb{S} \leftarrow \mathbb{E}_k$
\end{algorithmic}
\label{algorithm:LTI_RPI}
\end{algorithm}
For {\color{blue}practical implementation,} an outer $\epsilon$-approximation is usually used {\color{blue}for} the termination condition in line~\ref{al:eps} of an \Cref{algorithm:LTI_RPI} \cite{rakovic2005invariant}. Finally, the control input of the nominal MPC is computed with constraints tightened by the RPI set as follows:
\begin{equation} 
\begin{aligned} 
    \min_{\mathbf{z}_{(\cdot)},{\mathbf{\bar{u}}}_{(\cdot)}} \sum_{k=0}^{N-1}  l(&\mathbf{z}_k,\mathbf{\bar{u}}_k)+l_f(\mathbf{z}_N),   \\ 
    \text{s.t. } 
    \mathbf{z}_{k+1} &= A\mathbf{z}_k + B\mathbf{\bar{u}}_k,   \\
    \mathbf{z}_k &\in \mathbb{X} \ominus \mathbb{S},   \\
    \mathbf{\bar{u}}_k &\in \mathbb{U} \ominus K \mathbb{S}, \\
    \mathbf{z}_N &\in \mathbb{X}_f \ominus \mathbb{S},
\end{aligned}
\end{equation}
where $N$ is the prediction horizon, {\color{blue}$\mathbb S$ is the RPI set of the system \eqref{pre:error},} $l(\mathbf{z}_k,\mathbf{\bar{u}}_k)$ is the stage cost, $l_f(\mathbf{z}_N)$ is the terminal cost, and $\mathbb{X}_f$ is the terminal constraints.
% and the state-feedback control used in TMPC algorithm ensures that the actual system satisfies the original constraints under the bounded model uncertainty and disturbances. This also contributes to performance and stability.
