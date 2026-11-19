# Multi-Gate Validation Architecture and Results

## 1. Overview
Every periodic orbit candidate in **EM-CR3BP-NDA v1.0** is subjected to an exhaustive battery of 11 physical, numerical, and symplectic topological validation gates prior to inclusion in the archive. Failure of any single gate disqualifies the orbit.

---

## 2. Gate Definitions and Mathematical Thresholds

| Gate ID | Gate Name | Test Condition | Physical Significance | Threshold |
| :--- | :--- | :--- | :--- | :--- |
| **G1** | Periodicity Residual | $\|z(T) - z(0)\| \le \epsilon_p$ | Closure of trajectory in phase space | $\le 1.0 \times 10^{-11}$ |
| **G2** | Energy Conservation | $\max_{t} \|H(t) - H(0)\| \le \epsilon_H$ | Symplectic conservation of Jacobi integral | $\le 1.0 \times 10^{-12}$ |
| **G3** | Symplecticity Defect | $\|M^T \mathbb{J} M - \mathbb{J}\| \le \epsilon_{\text{sp}}$ | Monodromy matrix belongs to $\mathrm{Sp}(4)$ | $\le 2.0 \times 10^{-9}$ |
| **G4** | Determinant Condition | $\|\det(M) - 1\| \le \epsilon_{\det}$ | Volume preservation in Hamiltonian flow | $\le 2.0 \times 10^{-9}$ |
| **G5** | Trivial Multiplier | $\|(M - I) X_H(z_0)\| / \|X_H(z_0)\| \le \epsilon_{\text{triv}}$ | Velocity vector is Floquet eigenvector with $\lambda = 1$ | $\le 2.0 \times 10^{-9}$ |
| **G6** | Palindromic Residual | $\|\det(M - I)\| \le \epsilon_{\text{pal}}$ | Palindromic polynomial identity $\chi(1) = 0$ | $\le 2.0 \times 10^{-9}$ |
| **G7** | Reciprocal Multipliers | $\|\lambda_+ \lambda_- - 1\| \le \epsilon_{\text{rec}}$ | Symplectic spectrum pairing theorem | $\le 2.0 \times 10^{-9}$ |
| **G8** | Reduced Stability | $\|s_{\text{full}} - s_{\text{red}} - 2\| \le \epsilon_{\text{red}}$ | Consistency of normal bundle projection | $\le 1.0 \times 10^{-6}$ |
| **G9** | Topological Agreement | $\mu_{CZ}^{(\text{closed})} == \mu_{CZ}^{(\text{crossing})}$ | Closed-form polar lift matches Robbin–Salamon crossing form | Exact Integer ($0$) |
| **G10**| Lift Angular Resolution| $\max_{i} \|\Delta \phi_i\| \le \pi/4$ | Sampling density resolves winding number without aliasing | $\le \pi/4 \approx 0.7854$ |
| **G11**| A Posteriori Certificate| $\text{Certified} == \text{True}$ | Separation margin from singular boundary $\mathcal{D}$ | Margin $> 0$ |

---

## 3. Methodological Independence
Gate 9 enforces complete methodological independence:
- **Closed-form index** computes the continuous unwrap of the polar argument $w(t) = (a+d) + i(b-c)$ across the entire orbit.
- **Crossing-form index** locates exact interior zeros of $\operatorname{tr}(\Psi(t)) - 2 = 0$ and accumulates their quadratic crossing forms $\Gamma(v) = v^T \dot{\Psi}^T \mathbb{J} v$ together with the initial signature $\frac{1}{2}\operatorname{sign}(S(0))$.
- Agreement between these two fundamentally different numerical formulations guarantees that the reported Conley–Zehnder integer is mathematically certified.
