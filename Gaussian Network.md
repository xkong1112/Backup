PGM:
Probabilistic graphical model\
概率图模型

BN:
Bayesian Network\
贝叶斯网络

MN：
Markov Network\
马尔可夫网络

GN：
Gaussian Network\
高斯网络

```
graph LR
PGM-->BN
PGM-->GN
PGM-->MN
BN-->GBN有向
GN-->GBN有向
GN-->GMN无向
MN-->GMN无向
```


```math
x_i	\perp x_j \iff σ_{ij}=0
```
条件独立性：

```math
x_i	\perp x_j|_{-x_i,x_j} \iff λ_{ij}=0
```
精度矩阵，{-x_i,x_j}，条件是剩下所有的。也可以叫信息矩阵。\
Precision Matrix\
Information Matrix
```
graph LR

高斯网络-->高维的高斯分布
```