---
layout: single
title:  "Linear Parameter Varying System"
tags: [Modeling]
comments: true
author_profile: false
toc: true
---



## Linear Parameter Varying System

: State-space representations depend on exogenous nonstationary parameters.

$$
\begin{aligned}
\dot{x} &= A(p)x + B(p)u \\
y &= C(p)x
\end{aligned}
$$


> 아래의 경우 LPV-A 모델이라고도 부름. (A만 p에의해 바뀌는 모델) 
> > $$
\dot{x} = A(p)x + Bu 
$$


> LTV (Linear Time-Varying) 모델과의 차이점은?
>> (By ChatGPT)
![title](/fig/chatGPT.jpg){: width="500"}{: .align-center}








### **The process of identifying the state-space matrices of an LPV system using SIM method is as follows:**

1. Collect input-output data from the LPV system.
2. Form the Hankel matrix of the input-output data.
3. Use singular value decomposition (SVD) to decompose the Hankel matrix.
4. Estimate the system's state-space matrices from the SVD factors.
5. Verify the identified model using techniques such as cross-validation.











