# QSVT: Quantum Singular Value Transformation for Matrix Inversion

A gate-level implementation of **Quantum Singular Value Transformation (QSVT)** built in Python with **Qiskit**. This project demonstrates how to invert a block-encoded matrix by applying a $1/x$ polynomial transformation to its singular values using an alternating sequence of signal processing rotations.

---

## Technical Overview

QSVT acts as a grand unifying framework for quantum algorithms, achieving complex non-linear matrix transformations by interleaving a block-encoded unitary with parameterized single-qubit rotations. 

Key components of this implementation:
- **Polynomial Phase Sequence:** Utilizes a pre-calculated sequence of ~150 QSP phase angles designed to approximate the $f(x) = 1/x$ function. The sequence was generated for a condition number of $\kappa = 40$ and an approximation error of $\epsilon = 0.001$.[cite: 10]
- **Block Encoding ($U$):** Implements a custom 3-qubit unitary operator that encodes the target matrix into a larger quantum subspace using parameterized $R_Y$ rotations and $CX$ (CNOT) gates.
- **Signal Processing Iteration:** Alternates between applying the block encoding (or its inverse, $U^\dagger$) and applying $Z$-axis phase rotations ($R_Z(2\phi)$) on the helper qubit, bracketed by $X$ gates.
- **Statevector Tomography:** Simulates the circuit across the standard computational basis states to extract the successful amplitude components (where the helper qubit is measured as $0$). These amplitudes are systematically column-stacked to reconstruct the full classical matrix inverse.
- **Hardware Transpilation:** Automatically transpiles the algorithmic circuit down to a physical basis gate set (`cx`, `rz`, `sx`, `x`) to calculate the rigorous hardware depth required for execution.

---

## Circuit Specifications

- **Register Architecture:** 3 total qubits (1 Helper/Ancilla qubit, 2 Vector/Data qubits)
- **Algorithm Type:** Matrix Inversion ($1/x$)
- **Simulation Method:** Qiskit `AerSimulator` statevector backend

---

## Prerequisites

```bash
pip install qiskit qiskit-aer numpy pyqsp
