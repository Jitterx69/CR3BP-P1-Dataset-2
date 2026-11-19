# EM-CR3BP-NDA v1.0 — Final Archive Verification Report

## Executive Summary
- **Dataset Version**: `EM-CR3BP-NDA-v1.0` (Dataset-2)
- **Total Periodic Orbits Generated**: 694
- **Total Passing All 11 Archival Validation Gates**: 688 / 694 (99.1%)
- **Golden Subset Verified**: 18 orbits (100% topologically invariant across N/2, N, 2N)
- **Primary Model**: Planar Earth–Moon CR3BP ($\mu = 1.2150585609624 \times 10^{-2}$)

## Family Summaries

| Family Name | Orbit Count | Passing Count | C Range | T Range | $\mu_{CZ}$ | $\vartheta$ Range | Stability Type |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **$L_1$ Lyapunov** | 85 | 84 | [3.0488, 3.1883] | [2.6918, 3.5792] | 2 | 1.0000 | Positive Hyperbolic |
| **$L_2$ Lyapunov** | 112 | 107 | [2.9733, 3.1721] | [3.3733, 5.1634] | 2 | 1.0000 | Positive Hyperbolic |
| **DRO (f)** | 497 | 497 | [2.9759, 3.5282] | [0.1573, 1.9762] | 1 | [0.5000, 0.9746] | Elliptic |

## Archival Verification Gates
1. **Periodicity Residual**: $\|z(T) - z(0)\| \le 5.0 \times 10^{-11}$
2. **Energy Conservation**: $\max_t |H(t) - H(0)| \le 1.0 \times 10^{-11}$
3. **Symplecticity Defect**: $\|M^T \mathbb{J} M - \mathbb{J}\| \le 1.0 \times 10^{-8}$
4. **Determinant Residual**: $|\det(M) - 1| \le 5.0 \times 10^{-9}$
5. **Trivial Multiplier**: $\|(M - I) X_H(z_0)\| / \|X_H(z_0)\| \le 5.0 \times 10^{-9}$
6. **Palindromic Residual**: $|\det(M - I)| \le 5.0 \times 10^{-9}$
7. **Reciprocal Pair Residual**: $|\lambda_+ \lambda_- - 1| \le 5.0 \times 10^{-9}$
8. **Reduced Stability**: $|s_{\text{full}} - s_{\text{red}} - 2| \le 1.0 \times 10^{-4}$
9. **Topological Agreement**: Closed-form == Crossing-form exact match
10. **Lift Resolution**: $\max_i |\Delta \phi_i| \le \pi/4$
11. **A Posteriori Certificate**: Certified == True
