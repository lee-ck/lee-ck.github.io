---
layout: single
title:  "MPC Softwares"
tags: [MPC]
comments: true
author_profile: false
toc: true
---


MPC 구현할 때 자주 사용하는 Software List:

**NMPC**

> ACADO https://acado.github.io/
>> MATLAB 인터페이스 제공
>> 
>> Embedded system에 사용하기 좋음 

> acados https://docs.acados.org/
>> ACADO 후속 software - 더 빠르다고 하는데 ACADO도 충분히 빠름.

> CasADi https://web.casadi.org/
>> Interior-point (IPOPT) 이용 - 스케일이 큰 최적화 문제에 적합
>> (System identification 같이 많은 데이터를 이용하는 경우)
>>
>> 개인적으로 ACADO 보다 customize가 쉬움

**LMPC**

> CVX http://cvxr.com/cvx/
> 
> CVXPY https://www.cvxpy.org/
>
> CVXGEN https://cvxgen.com/docs/index.html
>
>> CVX 기반으로 MATLAB, Python, ... 에 사용할 수 있게 만든것들
>>
>> CVXGEN이 좋은듯..










