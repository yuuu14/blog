---
layout: post
title: KNN with Matrix Implementation
date: 2021-11-09 23:00 +0800
---
Given $X\_{test} \in \mathbf{R}^{m \times d}$, $X\_{train} \in \mathbf{R}^{n \times d}$  
Get distance matrix $M(i, j) = \text{distance}(X\_{test}[i], X\_{train}[j]) = (X\_{test}[i] - X\_{train}[j])^2$
$= X\_{test}^2[i] + X\_{train}^2[j] - 2 \times (X\_{test}[i] \cdot X\_{train}[j])$  
$M = (X\_{test}^2, \cdots, X\_{test}^2) + (X\_{train}^2, \cdots, X\_{train}^2)^{\mathrm{T}}$
$ - 2 \times (X\_{test} \cdot X\_{train}) \in \mathbf{R}^{m \times n}$

Using $M$, we can get the nearest $k$ neighbors of each sample in $X\_{test}$, then the prediction should be 
the most occuring class among them.

```python
class KNN():
    def __init__(self, X, Y, k):
        # train set for compare distance with test
        self.x_ = X.to(device)
        self.y_ = Y.to(device)
        self.k = k
        self.size_ = self.x_.shape[0]
        
    def predict(self, X, Y):
        # test set
        start = time.time()
        self.x = X.to(device)
        self.y = Y.to(device)
        self.size = self.x.shape[0]
        
        pow_x = torch.pow(self.x, 2).sum(1, keepdim=True).expand(self.size, self.size_)
        pow_x_ = torch.pow(self.x_, 2).sum(1, keepdim=True).expand(self.size_, self.size).transpose(0, 1)
        
        # distance matrix d_mat[i, j] = distance(x_test[i], x_train[j])
        #                             = x_test[i]**2 + x_train[j]**2 - 2*x_test[i]*x_train[j]
        d_mat = pow_x + pow_x_ - 2 * torch.matmul(self.x, self.x_.transpose(0, 1))
        orders = torch.argsort(d_mat)
        y_pred = []
        for order in orders:
            y_pred.append(np.bincount([self.y_[i] for i in order[:self.k]]).argmax())
        end = time.time()
        acc = torch.sum(torch.tensor(y_pred) == self.y.cpu()).item() / self.size
        print('k: {}, runtime: {:.4f}s'.format(k, end - start))
        print('accuracy on test set: {}'.format(acc))

```

# Reference
[1] https://blog.csdn.net/r1254/article/details/104888502
