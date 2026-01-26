
**Linear Programming**
**Projections**
- span
- basis
- affine set
	- does not pass through origin (zero vector)
- subspace
	- must contain a zero vector 
	- must pass addition and multiplication in a closed space
- norms
**Singular Value Decomposition** (**SVD** → used for transforming a matrix into smaller parts)
$A = UΣV^T$
- eigenvectors of $U=AA^T$ (m x m)
- non-zero singular values $\Sigma = diagonal \space matrix$ (n x n)
	- number of non-zero values makes up the rank
- the eigenvectors of $V = A^TA$ (m x n)
- low-rank matrix optimization
	- $k$ images with each image is $n^2$ pixels where $n = 5000$ → takes $k * n^2$ data which is too much 0 → using SVD to reduce size to $k*(2n+1)$
	- $A = U\Sigma V^T = [U^1, U^2, ..., U^r]\Sigma [V^1, V^2, ..., V^r]^T = [\sigma_1 U^1 V^1]^T + [\sigma_2 U^2 V^2]^T + ... + [\sigma_r U^r V^r]^T = 2n+1$
1. sensitivity analysis
	- 
2. low rank matrix approximations
3. data dimension reduction
**Gradient/Hessian**
$\nabla f = [\frac{d}{dx_1} \space \frac{d}{dx_2}]$
$\nabla^2 f = \begin{bmatrix} \frac{d^2}{dx_1^2} & \frac{d^2}{dx_1 dx_2}\\ \frac{d^2}{dx_2 dx_1} & \frac{d^2}{dx_2^2} \end{bmatrix}$
**Moore-Penrose Inverse**
- fat matrix (underdetermined)
	- $A^+ = A^T(AA^T)^{-1}$
- tall matrix (overdetermined)
	- $A^+ =(A^TA)^{-1}A^T$
**Ordinary Least Squares** (**OLS**)
**Frobenius Norm**
**Principle Component Analysis (PCA)**