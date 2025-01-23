---
title: Variational low bound  (ELBO)
date: 2025-01-23
summary: By maximizing the ELBO, the VAE optimizes both terms, ensuring good reconstruction quality while maintaining a well-structured latent space.
---
$$
L_\text{batch} = -\frac{1}{N} \sum_{i=1}^N \sum_{c=1}^C y_{\text{label},i,c} \log(y_{\text{pred},i,c})
$$
The variational lower bound (ELBO) is defined as:

$$
L_\text{VAE} = E_{q_\phi(z|x)} \left[ \log p_\theta(x|z) \right] - \text{KL} \left( q_\phi(z|x) \| p(z) \right)
$$

where:
- $ q_\phi(z|x) $: Approximate posterior distribution of the latent variable $ z $, parameterized by $ \phi $ (the encoder).
- $ p_\theta(x|z) $: Likelihood of the observed data $ x $, conditioned on $ z $, parameterized by $ \theta $ (the decoder).
- $E_{q_\phi(z|x)} $: Expectation with respect to $ q_\phi(z|x) $.
- $\text{KL} \left( q_\phi(z|x) \| p(z) \right)$: Kullback-Leibler divergence between $ q_\phi(z|x) $ and the prior $ p(z) $.
- $ p(z) $: Prior distribution of the latent variable $ z $ (commonly a standard Gaussian $ {N}(0, I) $).

**Interpretation:**
1. The term $ E_{q_\phi(z|x)} \left[ \log p_\theta(x|z) \right] $ encourages the model to reconstruct the input data $ x $ accurately from the latent variable $ z $.
2. The term $ \text{KL} \left( q_\phi(z|x) \| p(z) \right) $ regularizes the latent space by ensuring that the approximate posterior $ q_\phi(z|x) $ remains close to the prior $ p(z) $.
3. Maximizing $ L_{\text{VAE}} $ ensures a balance between accurate reconstruction and a smooth, interpretable latent space.


#### ELBO (Maximization Form)
The ELBO is defined as:
$$
L_{\text{VAE}} = E_{q_\phi(z|x)} \left[ \log p_\theta(x|z) \right] - \text{KL} \left( q_\phi(z|x) \| p(z) \right)
$$
- The goal is to maximize this objective.

#### VAE Loss (Minimization Form)
To convert it into a loss for minimization:
$$
\text{Loss} = -E_{q_\phi(z|x)} \left[ \log p_\theta(x|z) \right] + \text{KL} \left( q_\phi(z|x) \| p(z) \right)
$$
- The **likelihood term** $E_{q_\phi(z|x)}[\log p_\theta(x|z)]$ is positive in the ELBO, but negated to be part of the loss.
- The **KL divergence** is inherently non-negative, so it's directly added to the loss.

#### Why Minimize?
Minimizing this loss:
1. Encourages accurate reconstruction of  x  (by maximizing  $\log p_\theta(x|z)$ ).
2. Regularizes the latent space (by minimizing  $\text{KL}(q_\phi(z|x) \| p(z)$) ).

Thus, while the ELBO is maximized, the loss is its negative form, and we minimize it in practice.

