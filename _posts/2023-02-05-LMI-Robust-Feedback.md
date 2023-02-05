---
layout: single
title:  "Linear Matrix Inequality (LMI)"
tags: [MPC, Robust MPC]
last_modified_at: 2023-02-05T16:00+09:00
comments: true
author_profile: false
toc: true
---

$$
x_{t+1} = A(p_t)x_t + Bu_t 
$$

LPV-A 시스템을 stabilize할 수 있는 state feedback control gain K 찾기

$$
u_t = Kx_t
$$

"Quadratic stabilization"

$$
J = \sum_0^{\infty} x_t^\top Q x_t + u_t^\top R u_t
$$

worst case cost를 minimze할 수 있는 LMI problem:

$$
    \min_{P,K} \text{tr}(P)
$$

$$
    \text{s.t.} A^c(p)^\top P A^C(P) - P < -Q - K^\top R K
$$

where $A^c(p) = A(p) + BK$

LMI의 standard trick ($Y=P^{-1}, L=KY$)이용하여 convexification.

## Reference

[1] [https://yalmip.github.io/example/lpvstatefeedback/](https://yalmip.github.io/example/lpvstatefeedback/)