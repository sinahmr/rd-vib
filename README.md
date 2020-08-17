# Deep Variational Information Bottleneck by I(Z, X) Estimation

Based on the original code, provided by [paper](https://arxiv.org/abs/1612.00410) authors. Written in Tensorflow (< 2.0).

After experimenting with the code, I found out that the <img src="https://render.githubusercontent.com/render/math?math=I(Z, X)"> upper bound introduced in the paper and used in the code, is not really a tight bound.
So I estimated <img src="https://render.githubusercontent.com/render/math?math=I(Z, X)"> with sampling and used this quantity in the loss function.

As we know <img src="https://render.githubusercontent.com/render/math?math=I(Z, X) = H(X) - H(X | Z)">.
<img src="https://render.githubusercontent.com/render/math?math=H(X)"> is a constant, since we assume empircal data distribution in this paper, and it is equal to <img src="https://render.githubusercontent.com/render/math?math=\log N">.
<img src="https://render.githubusercontent.com/render/math?math=H(X | Z)"> can be estimated using a subsample of dataset (<img src="https://render.githubusercontent.com/render/math?math=M"> data points), because of the following equations:

<img src="https://render.githubusercontent.com/render/math?math=H(X | Z) = \mathbb{E}_{p(z, x)} [-\log p(x | z)] = -\mathbb{E}_{p(z, x)} [\log p(z | x) p(x) - \log \sum_{i=1}^{M} p(z | x_i) p(x_i)] = -\mathbb{E}_{x \sim p(x), z \sim p(z | x)} [\log p(z | x) - \log \sum_{i=1}^{M} p(z | x_i)]">
