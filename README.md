# Pi2_VerificationLab
[arXiv:2507.03107] Companion code for "A Constructive Heuristic Sieve for the Twin Prime Problem"
# Constructive Heuristic Sieve for Twin Prime Counting

[![arXiv](https://img.shields.io/badge/arXiv-2507.03107-b31b1b.svg)](https://arxiv.org/abs/2507.03107)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.15857682.svg)](https://doi.org/10.5281/zenodo.15857682)

Companion code for the paper:  
**"A Constructive Heuristic Sieve for the Twin Prime Problem"**  
by Yuhang Shi (Xi'an Qing'an Senior High School)

## 🔬 Research Focus
Implementation of the heuristic sieve model based on:
- Novel **$f(t;z)$ function analysis** (elementary symmetric polynomials of prime reciprocals)
- Series expansion of sieve correction factor $\mathcal{D}(z)$
- Numerical verification of twin prime counting function $\pi_2(x)$ approximations

> **Key Insight**: Demonstrates systematic overestimation in truncated series approximations, highlighting sensitivity to higher-order terms.

## 🛠️ Installation & Dependencies
```bash
# Python 3.8+ required
pip install -r requirements.txt
```
Dependencies:  
- `numpy` (for numerical operations)
- `sympy` (for prime number handling)
- `matplotlib` (optional for visualization)

## 📊 Reproducing Table 1 Results
To regenerate the $\pi_{2,\text{approx}}(x)$ data from Table 1:
```bash
python paper_data_verification.py
```

### Output Explanation
The script generates:
1. **Console table** matching Table 1 format
2. `results/table1.csv` with columns:
   - $x$ (upper bound)
   - $\pi_2(x)$ (true count)
   - $\pi_{2,\text{HL}}(x)$ (Hardy-Littlewood prediction)
   - $\pi_{2,\text{approx}}(x)$ (our model)
   - Relative errors

## 🧮 Core Functions
### `f(t, z)` Implementation
```python
def f(t: int, z: int) -> float:
    """
    Computes elementary symmetric polynomial of degree t
    in reciprocals of odd primes ≤ z
    
    Args:
        t: Polynomial degree (0 ≤ t ≤ 4)
        z: Sieving limit (e.g., z = floor(x^{1/4}))
    
    Returns:
        f(t;z) = Σ [1/(p₁p₂⋯pₜ)] for 3≤p₁<...<pₜ≤z
    """
```

### Correction Factor Calculation
```python
def D_approx(z: int) -> float:
    """
    Computes truncated sieve correction factor:
    𝒟_approx(z) = [Σ (-2)^t f(t;z)] / [Σ (-1)^t f(t;z)]^2 
                  for t=0 to 4
    """
```

## 📈 Key Findings (From Paper)
1. **Systematic overestimation** of $\pi_2(x)$ for $x \geq 10^6$
2. **Truncation sensitivity**:  
   $\mathcal{D}_{\text{approx}}(31) \approx 1.91$ vs actual $2C_2 \approx 1.32$ at $x=10^6$
3. **Error growth**: Relative error increases from +46.6% at $x=10^6$ to +177.6% at $x=10^7$

## 📖 Citation
```bibtex
@software{shi_pi2_verificationlab_2024,
  author       = {Shi, Yuhang},
  title        = {{Pi2\_VerificationLab}: Computational toolkit for twin prime sieve analysis},
  month        = jul,
  year         = 2025,
  publisher    = {Zenodo},
  version      = {v1.0.0},
  doi          = {10.5281/zenodo.15857682},
  url          = {https://doi.org/10.5281/zenodo.15857682}
}

## 📜 License
This project is licensed under the MIT License - see [LICENSE](LICENSE) for details.
```
