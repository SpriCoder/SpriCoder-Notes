Tec9-SVD
---
> 使用Python

# 1. Python使用SVD
```py
a = np.array([[0, 1], [1, 1], [1, 0]])
U,Sigma,VT = np.linalg.svd(a)
```

# 2. 选择奇异值重构图片
```py
sval_nums = 60
restruct1 = (U[:,0:sval_nums]).dot(np.diag(Sigma[0:sval_nums])).dot(VT[0:sval_nums,:])
```

# 3. 参考
1. <a href = "https://www.cnblogs.com/endlesscoding/p/10033527.html">SVD(奇异值分解)小结</a>