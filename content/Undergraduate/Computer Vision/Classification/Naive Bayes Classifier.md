
#### Equations
1. $$p(C_k|x_1, \cdots,x_n)=\frac{1}{Z}p(C_k)\prod_{i=1}^{n}p(x_i|C_k)$$
2. $$ \hat{y} = argmax_{k} \space p(C_k) \prod^n_{i=1}p(x_i|C_k) $$
#### Example
Distinguish children from adults based on height(cm), weight(kg) information.
- 4 adult, 12 children
- Suppose height, weight follows a normal distribution

1. define class: {a,c} (adult, children)
2. $P(a)=\frac{4}{4+12}$ , $P(b)=\frac{12}{4+12}$
3. $\mu_{h,a}=\frac{1}{4}\sum^{}_{i \in A}h_i$ , $\sigma_{h,a}=\frac{1}{4}\sum^{}_{i \in A}(h_i-\mu_{h,a})^2$ 
4. $\mu_{w,a}=\frac{1}{4}\sum^{}_{i \in A}w_i$ , $\sigma_{w,a}=\frac{1}{4}\sum^{}_{i \in A}(w_i-\mu_{w,a})^2$  
5. $\mu_{h,c}=\frac{3}{4}\sum^{}_{i \in C}h_i$ , $\sigma_{h,c}=\frac{3}{4}\sum^{}_{i \in C}(h_i-\mu_{h,c})^2$ 
6. $\mu_{w,c}=\frac{3}{4}\sum^{}_{i \in C}w_i$ , $\sigma_{w,c}=\frac{3}{4}\sum^{}_{i \in C}(w_i-\mu_{w,c})^2$  
7. $Adult_w \sim N(\mu_{w,a}, \sigma_{w,a}^2)$ , $Adult_h \sim N(\mu_{h,a}, \sigma_{h,a}^2)$
7. $Children_w \sim N(\mu_{w,c}, \sigma_{w,c}^2)$ , $Children_h \sim N(\mu_{h,c}, \sigma_{h,c}^2)$

Visual Image & Calculation Method

![[Pasted image 20231209164249.png|300]] ![[Pasted image 20231209164409.png|200]]

#### Limitations
1. Cannot tell correlation