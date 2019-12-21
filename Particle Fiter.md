### Monte Carlo 方法
拿到概率之后，更关心后验的期望。假如从

### Sequential Importance Filter 
问题就是权值退化，原因就是高维。
解决办法就是重采样，重采样就是在0-1之间均匀采样，但是每个样本根据权值大小来分配cdf，优胜劣汰。权值越大采样的数量也就越大。

==SIS + Resampling 就是 Baisc Particle Filter==

### SIR: Sampling Importance Resampling
基本的粒子滤波的过程
1. **Sampling:**\
用一个proposal dist + weight来代替原来的dist采样，对隐状态服从的分布进行简化，不然不好采样。\
这个proposal分布可以是任意的，也可以和分母的某一样一致，这样可以直接约分约掉。\
比如:
```math
q(z_t|z_{1:t-1},x_{1:t})=p(z_t|z_{t-1})
```
==generate and test==

```math
w_t^{(i)}=p(x_t|z_t^{(i)})w_{t-1}^{(i)}
```
概率越大，权重越大。符合逻辑。
2. **Normalized:**\
把权重的和加起来，总权重归一化为1。这样大权众对应的比例也越大。
3. **Resampling:**\
对于归一化之后的0-1空间均匀采样。

```
graph LR
IS-->SIS
SIS-->SR
```


