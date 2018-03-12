# Loss Function
用来评估预测值和实际值的差距。
The loss function quantifies the amount by which the prediction deviates from the actual values

## 损失项 loss item
回归问题：L2平方损失(linear regression)，L1绝对值损失
分类问题：hinge loss(for soft margin SVM)，log loss(for logistic regression)
hinge loss：L1 loss/squared hinge loss

hinge loss:
l(y) = max(0, 1 - m_i(w))
m_i(w)表示样本在模型预测下，第i个样本在模型下的预测值的类标记{-1, 1}的乘积。用于分类问题，可以用来检测分类是否正确。

log loss:
基于最大似然的负log
likehood = sum(y^i*log g_w(x^i) + (1-y^i)(log(1-g(x^i))))
l(y) = -likehood

## 正则项 regularization item
L0 非零数字的数量
L1 Manhattan norm 描述所有参数绝对值的和
L2 Euclidean norm 描述平方差
L-infinity norm 描述最大值


# 聚类方法
