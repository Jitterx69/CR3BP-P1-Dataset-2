# Earth–Moon CR3BP Periodic Orbit Numerical Dynamics Archive (EM-CR3BP-NDA v1.0)
## Complete High-Resolution Numerical Archive (Dataset-2)

[![DOI](https://zenodo.org/badge/1364467178.svg)](https://doi.org/10.5281/zenodo.24368897)

### Citation & Theoretical Foundation
Based on: *Mean rotation and Conley–Zehnder indices of planar periodic orbit families in the Earth–Moon system* (2026).

---

## 1. Executive Summary
**EM-CR3BP-NDA v1.0 (Dataset-2)** is an open, machine-readable, high-resolution scientific numerical archive of planar periodic orbits in the Earth–Moon circular restricted three-body problem.

The archive catalogs **790 periodic orbits** across the three primary planar families of the Earth–Moon system:
1. **$L_1$ Lyapunov Family**: 181 orbits emanating from the collinear equilibrium $L_1$ ($C \in [3.05, 3.1883]$).
2. **$L_2$ Lyapunov Family**: 112 orbits emanating from the collinear equilibrium $L_2$ ($C \in [2.9408, 3.1721]$).
3. **Distant Retrograde Orbit (DRO) Family**: 497 stable retrograde orbits about the Moon (Hénon family $f$, $C \in [2.4039, 3.5277]$).

For every orbit, the archive records:
- High-resolution trajectory time-series $(q_1, q_2, p_1, p_2)$ in canonical variables.
- Full fundamental matrix solution $\Psi(t) \in \mathrm{Sp}(4)$ and out-of-plane vertical variational solution $\Psi_v(t) \in \mathrm{Sp}(2)$.
- Symplectically reduced normal bundle path $\Psi^\gamma(t) \in \mathrm{Sp}(2)$.
- Conley–Zehnder index $\mu_{CZ}(\gamma)$ evaluated via dual independent algorithms (closed-form polar angle lift and Robbin–Salamon crossing forms).
- Mean rotation $\vartheta(\gamma)$, rotation number $\theta$, and Bott–Long iterate indices $\mu_{CZ}(\gamma^k)$ for $k = 1..8$.
- Exhaustive 11-gate physical and numerical validation certificates.

---

## 2. Directory Layout
```
EM-CR3BP-NDA-v1.0/
├── L1_Lyapunov_archive.h5    # 181 orbits with full variational histories
├── L2_Lyapunov_archive.h5    # 112 orbits with full variational histories
├── DRO_archive.h5            # 497 orbits with full variational histories
├── catalog/
│   ├── master_catalog.csv    # Flat tabular representation of all 790 orbits
│   └── master_catalog.json   # JSON representation
├── metadata/
│   └── MANIFEST.json         # Complete provenance, environment, and file manifests
├── CHECKSUMS.sha256          # Cryptographic SHA-256 hashes for all archive files
├── DATA_DICTIONARY.md        # Complete data schema and variable definitions
├── MODEL.md                  # Mathematical formulations, Hamiltonian, and reversibility
├── VALIDATION.md             # 11 validation gates, mathematical bounds, and certificates
└── REPRODUCIBILITY.md        # Instructions for running tests and recreating the archive
```

---

## 3. Quickstart (Python)
To inspect the archive:
```python
import h5py

with h5py.File("L1_Lyapunov_archive.h5", "r") as f:
    print(f"Family: {f.attrs['family']}, Count: {f.attrs['orbit_count']}")
    orb = f["orbits/L1_Lyapunov_0000"]
    print(f"Jacobi constant C: {orb.attrs['C']}")
    print(f"Period T: {orb.attrs['period']}")
    print(f"Conley-Zehnder index: {orb.attrs['cz_index']}")
    print(f"Mean rotation: {orb.attrs['mean_rotation']}")
    print(f"Trajectory samples shape: {orb['z'].shape}")
```
