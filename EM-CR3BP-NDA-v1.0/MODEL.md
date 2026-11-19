# Mathematical and Numerical Dynamics Model Specification

## 1. System Definition
The planar Earth–Moon Circular Restricted Three-Body Problem (CR3BP) describes the motion of an infinitesimal particle in the gravitational field of two primary bodies orbiting their common centre of mass in circular orbits.

### Equations of Motion
In Hamiltonian form:
$$\dot{q}_1 = \frac{\partial H}{\partial p_1} = p_1 + q_2$$
$$\dot{q}_2 = \frac{\partial H}{\partial p_2} = p_2 - q_1$$
$$\dot{p}_1 = -\frac{\partial H}{\partial q_1} = p_2 + \frac{\partial U}{\partial q_1}$$
$$\dot{p}_2 = -\frac{\partial H}{\partial q_2} = -p_1 + \frac{\partial U}{\partial q_2}$$

where the gravitational potential $U(q)$ is:
$$U(q) = \frac{1-\mu}{r_1} + \frac{\mu}{r_2}$$
$$r_1 = \sqrt{(q_1 + \mu)^2 + q_2^2}, \quad r_2 = \sqrt{(q_1 - 1 + \mu)^2 + q_2^2}$$

---

## 2. Reversible Symmetry
The system admits the reverser involution:
$$R = \operatorname{diag}(1, -1, -1, 1)$$
$$R(q_1, q_2, p_1, p_2) = (q_1, -q_2, -p_1, p_2)$$
satisfying:
$$H \circ R = H, \quad R^T \mathbb{J} R = -\mathbb{J}, \quad \Phi_t \circ R = R \circ \Phi_{-t}$$
Its fixed-point set is the 2-dimensional subspace:
$$\operatorname{Fix}(R) = \{q_2 = 0, \ p_1 = 0\}$$
Any orbit starting on $\operatorname{Fix}(R)$ that crosses $\operatorname{Fix}(R)$ again at $t = \tau > 0$ is guaranteed to be periodic with period $T = 2\tau$.

---

## 3. Variational Equations and Symplectic Structure
The state transition matrix $\Psi(t) = D\Phi_t(z_0)$ satisfies the linear Hamiltonian ODE:
$$\dot{\Psi}(t) = A(t) \Psi(t), \quad \Psi(0) = I_4$$
$$A(t) = \mathbb{J}_4 D^2 H(\gamma(t))$$
where:
$$\mathbb{J}_4 = \begin{pmatrix} 0 & I_2 \\ -I_2 & 0 \end{pmatrix}, \quad A(t)^T \mathbb{J}_4 + \mathbb{J}_4 A(t) = 0$$
$$\Psi(t)^T \mathbb{J}_4 \Psi(t) = \mathbb{J}_4, \quad \det \Psi(t) = 1$$

---

## 4. Symplectic Reduction and the Conley–Zehnder Index
Because $\gamma(t)$ is periodic, $X_H(\gamma(t))$ and $\nabla H(\gamma(t))$ generate two trivial Floquet multipliers at $\lambda = 1$.
The normal bundle along $\gamma$ is symplectically reduced using a canonical frame:
$$\Phi_\gamma(t) = \begin{pmatrix} \nu^{-1} X_H & \nu^{-1} \mathbb{J} X_H & \nu^{-1} \nabla H & \nu^{-1} \mathbb{J} \nabla H \end{pmatrix}$$
yielding the reduced path:
$$\Psi^\gamma(t) \in \mathrm{Sp}(2), \quad t \in [0, T]$$

The Conley–Zehnder index is calculated by two independent methods:
1. **Closed-Form Polar Angle Lift** (Theorem 23):
   $$w(t) = (a(t) + d(t)) + i(b(t) - c(t))$$
   $$\phi(t) = \arg w(t) \text{ (continuous lift, } \phi(0) = 0), \quad \Theta = \frac{\phi(T)}{2\pi}$$
   $$\mu_{CZ} = \begin{cases} 2\lfloor\Theta\rfloor + 1, & \operatorname{tr}(M^\xi) < 2 \text{ (elliptic / neg hyperbolic)} \\ 2\lfloor\Theta + \frac{1}{2}\rfloor, & \operatorname{tr}(M^\xi) > 2 \text{ (pos hyperbolic)} \end{cases}$$

2. **Crossing-Form Signature Count** (Robbin–Salamon Definition 9):
   $$\mu_{CZ} = \frac{1}{2}\operatorname{sign} S(0) + \sum_{0 < t_0 < T} \operatorname{sign} \Gamma(t_0)$$
