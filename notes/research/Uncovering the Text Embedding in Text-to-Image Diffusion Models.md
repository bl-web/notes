## 论文精读总结
### 关注的核心问题
1. 现有的图像生成，稍微修改prompt，可能会导致图像变化较大。
2. 且自然语言具有高度的抽象性，有时同一个prompt也会有不同的含义。

### 现有方法的缺陷
- 现有方法每次生成图像都需要我们额外训练模型，在内容保持方面也有不足。
- 由于text embedding在text和image之间起到桥梁作用，作者希望通过研究text embedding来实现可控的图像编辑和潜在语义方向的发现
### 解决方案A--无需学习的图像编辑
1. 单个token替换
$$
e_i^*= \begin{cases} e_i^t,&T_i^s\neq T_i^t\\ e_i^s,&\text{otherwise} \end{cases}
$$
2. 权重放缩
$$
 e_i^*= \begin{cases} c e_i^s,&i=j\\ e_i^s,&i\neq j \end{cases}
$$
3. semantic embedding与padding embedding的替换
-  具体实现如下图：
![[Pasted image 20261103160137.png]]
- 作者还用现有的优化框架--soft mixing weight of the source and target text embedding与自己的方法进行对比，进一步验证了无需学习的图像编辑方法的合理性。
### 解决方案B--探索text embedding在语义方向的潜力
- 作者通过SVD找出text embedding中具有特殊语义的方向，希望通过控制某个特殊语义方向来控制图像的编辑。
- 奇异值分解（SVD）公式：
$$
 E=U\Sigma V^T 
$$
- 根据某个语义方向的生成的新的embedding：
$$
e_{\text{sem}}= \begin{cases} e+P(e\cdot v),&\text{Right Vector}\\ e+P(u\cdot e),&\text{Left Vector} \end{cases}
$$
- 图像展示如下：
- ![[Pasted image 20261103162446.png]]
### 应用
- 用具体的例子来验证所提出方法的合理性。
- 与其他现有的方法进行比较，证明所提方法的优势。