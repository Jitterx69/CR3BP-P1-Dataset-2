# Reproducibility and Verification Protocol

## 1. Prerequisites
- Python 3.9+
- NumPy $\ge 1.20$
- SciPy $\ge 1.8$
- h5py $\ge 3.0$
- PyYAML $\ge 5.4$

All dependencies are standard scientific computing packages and can be installed via:
```bash
pip install numpy scipy h5py pyyaml pytest
```

---

## 2. Test Suite Execution
To verify the core physical model, symplectic matrices, reversibility invariants, Lagrange point equilibria, and integrators:
```bash
python3 -m pytest tests/test_model.py -v
```
All 36 unit tests should report `PASSED`.

---

## 3. End-to-End Single Orbit Verification
To generate and validate the three reference test orbits ($L_1$, $L_2$, and DRO) against paper parameters:
```bash
python3 test_single_orbits.py
```
This script computes:
- Newton convergence to machine precision
- Monodromy spectrum and palindromic conditions
- Full-period high-resolution propagation
- Symplectic reduction to $\mathrm{Sp}(2)$
- Dual closed-form and crossing-form Conley–Zehnder index verification
- Mean rotation and Bott–Long iterate indices ($k = 1..8$)
- Out-of-plane vertical monodromy and spatial Conley–Zehnder indices

---

## 4. Master Archive Generation
To reproduce the full 790-orbit archival generation:
```bash
python3 -m src.generate_archive
```

---

## 5. Checksum Verification
To verify archive integrity against SHA-256 checksums:
```bash
shasum -a 256 -c CHECKSUMS.sha256
```
