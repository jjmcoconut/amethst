1. Start with one pixel of potential region
2. Grow it by adding adjacent pixels until compared pixels are not similar

### RG-Grow Statistical Test

Given R: N pixel region, P: neighboring pixel

Define mean $\bar{X}=\frac{1}{N}\sum_{(r,c) \in R} I(r,c)$, sample variance $S^2 =\frac{1}{N}\sum_{(r,c) \in R}(I(r,c)-\bar{X})^2$ 

Define $T$ as
$$T=(\frac{(N-1)N}{N+1}(y-\bar{X})^2/S^2)^{1/2}$$

Then T has t distribution of N-1 degrees of freedom if all pixels in R and test pixel y are iid.

Pick a threshold $\alpha$ such that  
- If $T<\alpha$ then add test point y to region R and update $\bar{X}$ and $S^2$
- If $T>\alpha$ for every pixel, start a new region


