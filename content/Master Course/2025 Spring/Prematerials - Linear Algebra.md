
__Vector Space__ $V$
1. $\forall x,y\in V \rightarrow x+y\in V$
2. $\forall x\in V, \forall k \in \mathbb{R}\rightarrow k v\in V$
- Closed under linear combination ($k_1x_1+\cdots+k_nx_n\in V$)
- $V=\{0\}$ is vector space

__Subspace__ $W$
1. $W \subset V$
2. $W$ is vector space
- Ex) $V=\mathbb{R}^2$, $W_1=\{(x,y)^T:y=2x\}$
	- $W_1\subset V$
	- Vector space
		1. $\forall (x_1,y_1)\in W_1$, $\forall (x_2,y_2)\in W_1$ 
		   $y_1+y_2=2x_1+2x_2=2(x_1+x_2)$, $(x_1+x_2,y_1,y_2)\in W_1$
		2. $\forall (x_1,y_1)\in W_1, \forall k \in \mathbb{R}$
		   $ky_1=k\cdot2x_1=2\cdot kx_1,(kx_1,ky_1)\in W_1$

__Span__
- Given fixed $u_1,\dots,u_n\in V$ define __span__ $W=\mathcal{L}(u_1,\dots,u_n)$: $W=\{x:x=\sum_{i=1}^n\alpha_i u_i,\alpha_i\in\mathbb{R}\}$, set of all linear combinations of $u_i$. 
- If $\{u_1,\dots,u_n\}$ spans V, $\{u_1,\dots,u_n\}$ is a __spanning set__ of V

__Basis__
1. $\{ u_1,\dots, u_n \}$ is linearly independent
2. $V=\mathcal{L}(u_1,\dots,u_n)$
- Ex) $\mathbb{R}^3$'s basis: $\{(0,0,1),(0,1,0),(1,0,0)\}$
- Evry vector in $V$ has a unique representation of a given basis
	- Let $\{u_1,\dots,u_n\}$ be basis of $V$
	- Suppose two sets of coefficients satisfies $x=\sum a_iu_i=\sum b_iu_i$
	- $0=\sum(a_i-b_i)u_i \iff a_i=b_i$ for all $i$ (linearly independent)

__Dimension__
- Number of vectors in any basis of $V$
- Maximum number of linear independent vectors in $V$

__Inner Product__
- $\forall u,v\in V,\forall c\in \mathbb{R}$ define $<\cdot,\cdot>\:V\times V\rightarrow \mathbb{R}$
	1. $u\cdot u\geq 0$
	2. $u\cdot v = v \cdot u$
	3. $(u+v)\cdot w = u\cdot w + v\cdot w$
	4. $(cu)\cdot v=c(u\cdot v)$

__Norm__
$\|u\|$ is a vector __norm__ on iff $\forall u,v \in V,\forall \alpha\in\mathbb{R}$
1. $\|u\|\geq0$
2. $\|u\|=0\iff u=0$
3. $\|\alpha u\|=\alpha \|u\|$
4. $\|u+v\|\leq\|u\|+\|v\|$
	- $\|u\|_p=(\sum |u_i|^p)^{1/p}$
	- $\|u\|_\infty = \max(u_i)$
	- $\|u\|_0 = \sum I(u_i\neq 0)$

__Distance__
$d(u,v)$: distance iff $\forall u,v,w\in V$
1. $d(u,v)\geq 0$
2. $d(u,v)=0 \iff u=v$
3. $d(u,v)=d(v,u)$
4. $d(u,w)\leq d(u,v)+d(v,w)$

__Orthogonal Vectors__
$u,v\in \mathbb{R}^n$ are orthogonal if $u\cdot v=0$


__Projection__
- $p(u|v)$: projection of $u$ onto $v$ if
	1. $p(u|v)=bv$ for some constant $b\in\mathbb{R}$
	2. $u-p(u|v)$ is orthogonal to $v$
- $(u-bv)\cdot v=0 \Rightarrow b=\frac{u\cdot v}{\|v\|^2}$
- Among all $\alpha v$ $(\alpha \in \mathbb{R})$, $p(u|v)$ is the closest to $u$
	- pf) $b=\min_\alpha \|u-av\|^2=\|u-p(u|v)\|^2+\|p(u|v)-\alpha v\|^2$

__Projection onto a Subspace__
- $p(u|V)$: a projection of $u$ onto subspace $V$
	1. $p(u|V)\in V$
	2. $u-p(u|V)\perp V$ ($x\perp V \iff x\perp y, \forall y\in V$)
- Orthogonal basis of vectors: __Gram-Schmidt__


__Orthogonal Complement of a Subspace__
- $V^\perp=\{x:x\in \mathbb{R}^n,x\perp V\}$
- This is a subspace: $\forall x_1,x_2 \in V^\perp,\forall v\in V$
	- $(x_1+x_2)\cdot v=x_1\cdot v +x_2\cdot v=0$
	- $kx_i\cdot v =0$
- For any $x\in\mathbb{R}^n$, $\exists u\in V,v\in V^\perp$ s.t. $x=u+v$
	- pf) Find orthonormal basis of $\mathbb{R}^n:\{u_1,\dots,u_r,u_{r+1},\dots,u_n\}$
	- $\forall x \in \mathbb{R}^n$: $x=a_1u_1+\cdots+a_ru_r+\cdots+a_{r+1}u_{r+1}+\cdots+a_nu_n=u+v$


__Column Space $\mathcal{C}(A)$__ 
- Subspace of $\mathbb{R}^m$ spanned by columns of $A$
	- $\mathcal{L}(a_1,\dots,a_n)$
	- $\{Ac,c\in\mathbb{R}^n\}$
- Row rank = Column rank (dim(C(A))=dim(R(A)))
	- Let $r$= row rank, $R(A)$ has basis $\{ x_1,\dots,x_r \}$, show $\{Ax_1,\dots,Ax_r\}$ is linearly independent
		- Set $\sum_{i=1}^r c_i Ax_i=0\Rightarrow A(\sum_{i=1}^r c_ix_i)=0$
		- $Av=0 \Rightarrow v\perp \text{each row of }A\Rightarrow v\perp R(A)$
		- $v=0 \Rightarrow \sum c_ix_i=0 \Rightarrow c_i=0 \forall i$
		- There exists at least r linearly independent vectors in $\mathcal{C}(A)\Rightarrow$ dim$(C(A))\geq r$
		- dim$(C(A))\geq$ dim$(\mathcal{R}(A))$
		- isw dim$(R(A))\geq$ dim$(\mathcal{C}(A))$
- If $r(A)=r$, $\exists B:m\times r, T: r\times n$ both full rank s.t. $A=BT$
	- pf) C(A) has $r$ basis vectors, put them into a $m\times r$ matrix $B$
	- Each column of $A$: $a_i$, $a_i=By_i$
	- $A=[a_1,\cdots,a_n]=[By_1,\cdots,By_n]=B[y_1,\cdots,y_n]=BT$
	- $r(B)=r$
	- $r=r(A)=r(BT)\leq r(T)\leq r\Rightarrow r(T)=r$
- $C(AB)\subset C(A)$
	- $AB$ has columns $Ab_1,\dots,Ab_q$ which all belongs to $\mathcal{C}(A)$ 
- $C(A^TA)=C(A^T)$

__Null Space of A__
- $N(A)=\{x:Ax=0\}$

__SIngular__
- If a square matrix $A\in\mathbb{R}^{n\times n}$ has $r(A)=n$ it is non-singular, if $r(A)<n$ it is singular

__Trace__
- $tr(A)=\sum_i a_ii$
- $tr(AB)=tr(BA)$
- $tr(ABC)=tr(BCA)=tr(CAB)$
- $tr(A^TA)=tr(AA^T)=\sum_{i,j}a_{ij}^2\geq0$
	- $tr(A^TA)=0 \iff A=0 \iff A^TA=0$
- $AB=AC \iff A^TAB=A^TAC$
	- ($\Leftarrow$) $tr((AB-AC)^T(AB-AC))=tr((B-C)^T(A^TAB-A^TAC))=0$
- $C(A^T)\subset C(A^TA):C(A^TA)^\perp\subset C(A^T)^\perp$
	- let $y\in C(A^TA)^\perp \Rightarrow y^TA^TA=0\Rightarrow y^TA^T=0\Rightarrow y\in C(A^T)^\perp$
	- isw $R(A)=R(A^TA)$...
	- $\Rightarrow r(A)=r(A^TA)=r(AA^T)=r(A^T)$

__Linear System__
- $Ax=b$
	- When such $x$ exists, system is consistent $\iff b\in C(A)$
- If A has full row rank ($r(A)=m$), $Ax=b$ is consistent
	- $dim(C(A))=m \Rightarrow C(A) =\mathbb{R}^m$
- $A^TAx=A^Tb$ is always consistent
	- $\because A^Tb\in C(A^T)=C(A^TA)$
- If A has full column rank $r(A)=n,R(A^TA)=n$, nonsingular, x is unique: $x=(A^TA)^{-1}A^Tb$

__Idempotent Matrix__
- $A^2 = AA=A$
- The only non-singular idempotent matrix is $I$
- Singular idempotent matrix example
	- $$\left(\frac{1}{n}J\right)^2=\frac{1}{n^2}\begin{bmatrix} 1 & 1 & 1 & \cdots & 1 \\ 1 & 1 & 1 & \cdots & 1 \\ 1 & 1 & 1 & \cdots & 1 \\ \vdots & \vdots & \vdots& \ddots & \vdots \\ 1 & 1 & 1 & \cdots & 1 \end{bmatrix}^2=\frac{1}{n}J$$
- $A^T$ is also idempotent
	- $A^TA^T=(AA)^T=A^T$
- $I-A$ is also idempotent
	- $(I-A)(I-A)=I-2A+AA=1-2A+A=1-A$
- $A^3=A^4=\cdots=A^m=A$
- For any $A\in\mathbb{R}^{m\times n}$, $AA^-,A^-A$ are idempotent
	- $AA^-AA^-=AA^-$
- $r(A)=tr(A)$
	- If $A$ has full column rank and row rank $B=C\iff ABD=ACD$
		- If $A$ has full column rank $B=C \iff AB=AC$
		- If $A$ has full row rank $B=C \iff BA=CA$
	- $\exists B\in \mathbb{R}^{n\times r},\exists T \in \mathbb{R}^{r\times n}$ s.t. $A=BT$
		- $A^2=A \iff BTBT=BIT \iff TB=I_r$
		- $tr(A)=tr(BT)=tr(TB)=tr(I_r)=r=r(A)$
- $A$: idempotent $\iff$ $N(A)=C(I-A)$ 
	- ($\Rightarrow$) $\forall x \in N(A)$, $Ax=0 \iff x-Ax=x \iff x=x-Ax=(I-A)x\in C(I_A)$
	  $\forall x\in C(I-A)$, $\exists y: x=(I-A)y \iff Ax=A(I-A)y=(A-A^2)y=0 \iff x\in N(A)$
	- ($\Leftarrow$) $\forall x \in \mathbb{R}^n$, $(I-A)x\in C(I-A)\Rightarrow (I-A)x\in N(A)\Rightarrow A(I-A)x=0$ 
		- $\Rightarrow A(I_A)=0 \Rightarrow A^2=A$


__Projection Matrix__
- Let $z=p(y|C(X))$ be projection of $y$ onto $C(X)$
	- $z\in C(X)\Rightarrow \exists b\in\mathbb{R}^n$ s.t. $z=Xb$
	- $y-z \perp C(X) \Rightarrow y-Xb\perp C(X)\Rightarrow X^T(y-Xb)=0\Rightarrow X^TXb=X^Ty$
	- $\Rightarrow z=Xb=X(X^TX)^-X^Ty=P_xy\Rightarrow P_x=X(X^TX)^-X^T$
- Properties
	- $P_xX=X$: $(X^TX)^-X^T$ is a general inverse of $X$
	- $P_x$ is symmetric
	- $X^TP_x=X^T$
	- $P_x$ is idempotent
		- $P_x^2=[X(X^TX)^-X^TX](X^TX)^-X^T=[X](X^TX)^-X^T$ by $P_xX=X$
	- $C(P_x)=C(X)$
		- $P_x=X(X^TX)^-X^T \Rightarrow C(P_x)\subset C(X)$ is trivial
		- $C(X)=C(P_xX)\subset C(P_x)$
	- $r(P_x)=r(X)$
	- $I-P_x$ is the projection matrix to $C(X)^\perp$
		- $\forall y\in\mathbb{R}^n$, $y=p(y|C(X))+p(y|C(X))^\perp=P_xy+(I-P_x)y$
	- $A$ is symmetric and idempotent $\iff$ $A$ is a projection matrix
		- ($\Leftarrow$) Obvious
		- ($\Rightarrow$) $P_A=A(A^TA)^-A=A(AA)^-A=AA^-A=A$: $A$ is projection mtx to $C(A)$

__Determinant__
- Submatrix $A_{-i,-j} \in\mathbb{R}^{(n-1)\times (n-1)}$ by deleting $i$th row and $j$th column
- Co-factor $A_{ij}=(-1)^{i+j}det(A_{-i,-j})$
- $|A|=det(A)=\sum_{j=1}^n a_{ij}A_{ij}=\sum_{i=1}^na_{ij}A_{ij}$ (for any fixed i, j respectively)
- Properties
	- $|A|=|A^T|$
	- If two rows or columns are identical $det=0$
	- $A$ is nonsingular $\iff$ $|A|\neq0$
	- If two rows or columns are switched: $|A|\rightarrow -|A|$
	- $|AB|=|BA|$
	- $|A^TA|=|AA^T|\geq0$
	- If a row or column is 0, $|A|=0$
	- $A$: diagonal $\rightarrow$ $|A|=\prod_{i=1}^n a_{ii}$ 
		- $|cA|=c^n|A|$
	- $A$: triangular $\rightarrow$ $|A|=\prod_{i=1}^n a_{ii}$  
	- $A=\begin{bmatrix} A_{11}&A_{12}\\A_{21}&A_{22} \end{bmatrix}\Rightarrow$ If $A_{12}=0$ or $A_{21}=0$, $|A|=|A_{11}||A_{22}|$

__Inverse__
- Adjoint $A^*={A_{ij}}^T$: Transpose of matrix of cofactor $(-1)^{i+j}|A_{-i,-j}|$
- $A^{-1}=\frac{1}{|A|}A^*$
- Properties
	- $|A^{-1}|=|A|^{-1}$
	- $A$ nonsingular symmetric $\Rightarrow$ $A^{-1}$ nonsingular, symmetric
		- $AA^{-1}=I$
		- $(A^{-1})^TA^T=I^T=I$
		- $A^T$ is inverse of $(A^{-1})^T$
		- $(A^{-1})^T=(A^T)^{-1}=A^{-1}$
	- $(aI+bJ)^{-1}=\frac{1}{a}I+\frac{-b}{a(a+nb)}J$
	- $A=\begin{bmatrix} A_{11}&0\\0&A_{22} \end{bmatrix}\Rightarrow A^{-1}=\begin{bmatrix} A_{11}^{-1}&0\\0&A_{22}^{-1} \end{bmatrix}$
	- $A=\begin{bmatrix} A_{11}&A_{12}\\A_{21}&A_{22} \end{bmatrix}\Rightarrow A^{-1}=\begin{bmatrix} A_{11\cdot2}^{-1}&-A_{11}^{-1}A_{12}A_{22\cdot 1}^{-1}\\-A_{22}^{-1}A_{21}A_{11\cdot 2}^{-1}&A_{22\cdot 1}^{-1} \end{bmatrix}$
		- $A_{11\cdot 2}=A_{11}-A_{12}A_{22}^{-1}A_{21}$
		- $A_{22\cdot1}=A_{22}-A_{21}A_{11}^{-1}A_{12}$

__Quadratic Form__
- Let $A\in\mathbb{R}^{n\times n},x\in\mathbb{R}^n$, $x^TAx=\sum_{i,j}a_{ij}x_ix_j$
- Notes
	- There always exists a symmetric matrix that has the same quadratic form $x^TAx=x^TBx$
	- $A,B$: symmetric then $x^TAx=x^TBx\iff A=B$
	- A:symmetric then $\forall x, x^TAx=0 \iff A=0$
	- 