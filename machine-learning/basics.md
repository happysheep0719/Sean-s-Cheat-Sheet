# Loss Function
用来评估预测值和实际值的差距。
The loss function quantifies the amount by which the prediction deviates from the actual values

## 损失项 loss item
回归问题：L2平方损失(linear regression)，L1绝对值损失
分类问题：hinge loss(for soft margin SVM)，log loss(for logistic regression)
hinge loss：L1 loss/squared hinge loss

## 正则项 regularization item
L0 非零数字的数量
L1 Manhattan norm 描述所有参数绝对值的和
L2 Euclidean norm 描述平方差
L-infinity norm 描述最大值