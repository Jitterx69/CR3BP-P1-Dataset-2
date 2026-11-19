# EM-CR3BP-NDA v1.0 — Data Dictionary

## 1. Overview
This data dictionary defines all datasets, attributes, variables, coordinate frames, units, and conventions used across the **Earth–Moon CR3BP Periodic Orbit Numerical Dynamics Archive (EM-CR3BP-NDA v1.0, Dataset-2)**.

---

## 2. Coordinate System and Canonical Variables
The dynamics are formulated in the planar circular restricted three-body problem with the Earth and Moon as primaries.

- **Coordinate Frame**: Barycentric synodic (co-rotating) coordinate frame $(q_1, q_2)$.
- **Origin**: Barycentre of the Earth–Moon system.
- **Orientation**:
  - $q_1$-axis: Points from the Earth to the Moon.
  - $q_2$-axis: In the orbital plane of the primaries, completing a right-handed system.
- **Physical Normalization**:
  - Distance between primaries: $L = 1$ ($3.844 \times 10^5\text{ km}$).
  - Total mass $M_1 + M_2 = 1$.
  - Angular velocity of rotating frame: $\omega = 1$.
  - Synodic period of primaries: $2\pi$.
  - Gravitational mass parameter: $\mu = 1.2150585609624 \times 10^{-2}$.
  - Earth position: $(-\mu, 0) = (-0.012150585609624, 0)$.
  - Moon position: $(1 - \mu, 0) = (0.987849414390376, 0)$.

- **Canonical State Vector**:
  $$z = (q_1, q_2, p_1, p_2) \in \mathbb{R}^4$$
  where canonical momenta are related to synodic velocities $\dot{q} = (\dot{q}_1, \dot{q}_2)$ by:
  $$p = \dot{q} - \mathbb{J}_2 q \iff p_1 = \dot{q}_1 - q_2, \quad p_2 = \dot{q}_2 + q_1$$
  $$\mathbb{J}_2 = \begin{pmatrix} 0 & 1 \\ -1 & 0 \end{pmatrix}$$
  Here $p$ represents the inertial velocity expressed in synodic coordinates.

- **Hamiltonian and Jacobi Constant**:
  $$H(q, p) = \frac{1}{2} \|p\|^2 + p \cdot (\mathbb{J}_2 q) - U(q)$$
  $$U(q) = \frac{1-\mu}{r_1} + \frac{\mu}{r_2}, \quad r_1 = \|q - (-\mu, 0)\|, \quad r_2 = \|q - (1-\mu, 0)\|$$
  $$C = -2H$$

---

## 3. HDF5 Archive Hierarchy

Each archive file (`L1_Lyapunov_archive.h5`, `L2_Lyapunov_archive.h5`, `DRO_archive.h5`) contains the following hierarchical schema:

### Root Attributes
| Attribute Name | Type | Description |
| :--- | :--- | :--- |
| `dataset_name` | String | Full title of archive |
| `dataset_version` | String | `EM-CR3BP-NDA-v1.0` |
| `family` | String | Orbit family name |
| `orbit_count` | Integer | Total number of periodic orbits in the file |
| `timestamp_utc` | String | UTC ISO-8601 generation timestamp |
| `mu` | Float64 | Earth–Moon mass ratio |
| `coordinate_frame` | String | `Synodic barycentric rotating` |
| `state_convention` | String | `z = (q1, q2, p1, p2)` |
| `hamiltonian` | String | Analytical Hamiltonian definition |
| `reverser` | String | `R = diag(1, -1, -1, 1)` |

### Orbit Group `/orbits/{family}_{index:04d}`
Each group represents a single validated periodic orbit:

#### Attributes
| Attribute | Type | Description |
| :--- | :--- | :--- |
| `orbit_id` | String | Unique orbit identifier (e.g. `L1_Lyapunov_0042`) |
| `index` | Int | Member index within family |
| `period` | Float64 | Minimal orbital period $T$ |
| `tau` | Float64 | Half-period $\tau = T/2$ |
| `C` | Float64 | Jacobi constant $C = -2H$ |
| `H` | Float64 | Energy value $H(z_0)$ |
| `stability_index` | Float64 | Planar stability index $s = \operatorname{tr}(M) - 2$ |
| `reduced_stability` | Float64 | Reduced Sp(2) stability index $s_\xi = \operatorname{tr}(M^\xi) - 2$ |
| `cz_index` | Int | Conley–Zehnder index $\mu_{CZ}(\gamma)$ |
| `mean_rotation` | Float64 | Mean rotation $\vartheta(\gamma)$ |
| `stability_type` | String | `elliptic`, `positive_hyperbolic`, or `negative_hyperbolic` |
| `all_gates_passed` | Bool | `True` if all 11 archival validation gates passed |

#### Datasets
| Dataset | Shape | Dtype | Description |
| :--- | :--- | :--- | :--- |
| `z0` | `(4,)` | Float64 | Initial canonical state $(q_1, 0, 0, p_2)$ on $\operatorname{Fix}(R)$ |
| `t` | `(N+1,)` | Float64 | Uniform sample times $t \in [0, T]$ |
| `z` | `(N+1, 4)` | Float64 | High-resolution trajectory states along the orbit |
| `Psi` | `(N+1, 4, 4)` | Float64 | State transition matrix history $\Psi(t) \in \mathrm{Sp}(4)$ |
| `Psi_v` | `(N+1, 2, 2)` | Float64 | Decoupled out-of-plane vertical variational STM history |
| `reduced_path` | `(N+1, 2, 2)` | Float64 | Symplectically reduced normal bundle path $\Psi^\gamma(t) \in \mathrm{Sp}(2)$ |

#### Group `validation_gates/`
Contains subgroups for each of the 11 gates (`periodicity`, `energy_drift`, `symplectic_defect`, `determinant`, `trivial_multiplier`, `palindromic`, `reciprocal_pair`, `reduced_stability`, `cz_agreement`, `lift_resolution`, `certificate`) storing their exact evaluated residuals, numerical thresholds, and pass/fail booleans.
