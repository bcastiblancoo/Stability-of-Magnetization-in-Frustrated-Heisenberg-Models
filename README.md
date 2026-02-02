# Stability-of-Magnetization-in-Frustrated-Heisenberg-Models
Computation of staggered magnetization in 2D square and 3D simple-cubic Heisenberg antiferromagnets using Linear Spin-Wave Theory and Duffy-regularized Brillouin-zone integrals. Framework designed for extension to frustrated (J_1 - J_2)models.

This work is currently carried out at Aarhus University under the supervision of Prof. Dr. Georg Bruun, in the context of the "Individual Project in Physics" course in the MSc Physics program. It is also intended to present as a poster in the "Workshop on Impurity Problems in Quantum Mixtures: from Ultracold Gases to Electron Matter | (smr 4208)" at the ICTP, in Trieste, Italy, during 23-25 Feb 2026.

# Magnetization in Antiferromagnetic Heisenberg Lattices

This repository contains the theoretical formulation and numerical implementation
of a framework to compute the **ground-state staggered magnetization** of quantum
Heisenberg antiferromagnets using **Linear Spin-Wave Theory (LSWT)** combined with
**Duffy-regularized momentum-space integrals**.

The current implementation focuses on the **nearest-neighbor spin-1/2 Heisenberg
antiferromagnetic model** on:
- the **2D square lattice**, and
- the **3D simple-cubic lattice**.

The framework is designed to be systematically extended to **frustrated
next-nearest-neighbor \(J_1\!-\!J_2\)** Heisenberg models, where magnetic order is
destabilized by frustration.

---

## Motivation

In quantum antiferromagnets, zero-point fluctuations strongly reduce the staggered
magnetization from its classical value. Within LSWT, this reduction is expressed
as an integral over the **Magnetic Brillouin Zone (MBZ)**, which exhibits infrared
singularities at the Goldstone points.

Standard numerical integration schemes struggle with these singularities.
In this project, **Duffy coordinate transformations** are used to regularize the
integrals by mapping the MBZ onto unit simplices, allowing stable and accurate
high-order Gauss–Legendre quadrature.

This approach reproduces known benchmark results from series expansions and
quantum Monte Carlo simulations, while remaining conceptually simple and
computationally efficient.

---

## Implemented Models

### Nearest-neighbor Heisenberg antiferromagnet (current scope)

The Hamiltonian considered is

\[
\hat{H} = J \sum_{\langle i,j \rangle} \hat{\mathbf{S}}_i \cdot \hat{\mathbf{S}}_j,
\quad J > 0,
\]

with spin \(S = \tfrac{1}{2}\).

Implemented cases:
- **2D square lattice**
  - Coordination number \(q = 4\)
  - MBZ: diamond-shaped region
- **3D simple-cubic lattice**
  - Coordination number \(q = 6\)
  - MBZ: octahedral region

For both cases:
- Holstein–Primakoff and Bogoliubov transformations are applied
- Magnon dispersion relations are derived analytically
- The staggered magnetization is computed as a momentum-space integral over the MBZ
- Duffy transformations regularize the infrared singularities

---

## Numerical Method

The MBZ integrals are evaluated by:

1. Exploiting lattice symmetries to reduce the MBZ to a single simplex
   - 2D: right triangle
   - 3D: tetrahedron
2. Applying Duffy mappings to transform the simplex to the unit hypercube
3. Using tensor-product Gauss–Legendre quadrature on \([0,1]^d\)

This yields stable numerical values for the staggered magnetization:
- **2D square lattice:** ⟨S⟩ ≈ 0.3034
- **3D simple-cubic lattice:** ⟨S⟩ ≈ 0.4216

in excellent agreement with established results in the literature.

---

## Planned Extensions

The framework is intentionally modular and will be extended to include:

- **Frustrated \(J_1\!-\!J_2\) Heisenberg models**
  - Next-nearest-neighbor interactions
  - Square lattice as primary target
- Analysis of the **stability of Néel order** as a function of frustration
- Identification of parameter regimes where long-range magnetic order collapses
- Possible comparison with known phase boundaries from high-precision studies

---

## Repository Structure

```text
│
├── figures/
│
├── report-BECO_IndividualProject.pdf
│
└── README.md

