# Quantum Computing Roadmap

 ![License](https://img.shields.io/badge/license-MIT-green.svg) ![language](https://img.shields.io/badge/language-python-blue.svg) ![tools](https://img.shields.io/badge/tools-qiskit%20%7C%20pennylane%20%7C%20cirq-purple.svg)

From qubits and linear algebra to Grover, Shor, variational algorithms, and error correction, with every concept checked by a simulator you write or run.

## Table of Contents

1. [Workflow Overview](#workflow-overview)
2. [Prerequisites](#prerequisites)
3. [Phase 1: Foundations](#phase-1-foundations)
4. [Phase 2: Circuits & Simulators](#phase-2-circuits--simulators)
5. [Phase 3: Quantum Algorithms](#phase-3-quantum-algorithms)
6. [Phase 4: Variational & Quantum ML](#phase-4-variational--quantum-ml)
7. [Phase 5: Error Correction & Hardware](#phase-5-error-correction--hardware)
8. [Capstone Projects](#capstone-projects)
9. [Repository Layout](#repository-layout)
10. [Engineering Rules](#engineering-rules)
11. [Exit Criteria](#exit-criteria)

---

## Workflow Overview

```
 Qubits + linear algebra --> Gates + circuits --> Quantum algorithms
                                                        |
 Error correction + hardware <-- Variational / QML <----+
          |
          +--> Post-quantum cryptography (links to the Cybersecurity roadmap)
```

## Prerequisites

- [ ] Linear algebra: complex vectors, inner products, eigenvalues (Stages 0 and 3 of the ML roadmap)
- [ ] Complex numbers and basic probability
- [ ] Python and NumPy

## Phase 1: Foundations

Goal: Learn the postulates as linear algebra.

| Resource | Type | Why |
|----------|------|-----|
| [Quantum Country](https://quantum.country/) | Interactive essay | Spaced repetition builds retention |
| [John Preskill's Quantum Computation Notes](http://theory.caltech.edu/~preskill/ph229/) | Lecture notes | Rigorous and concise |
| [Quirk](https://algassert.com/quirk) | Simulator | Drag-and-drop circuit intuition |

- [ ] States, superposition, measurement, and the Bloch sphere
- [ ] Tensor products and entanglement; Bell states
- [ ] Density matrices and mixed states

**Deliverables**
- [ ] `notebooks/foundations/` with hand-computed examples checked in NumPy

## Phase 2: Circuits & Simulators

Goal: Build and run circuits, starting with your own simulator.

| Resource | Type | Why |
|----------|------|-----|
| [Qiskit Documentation](https://docs.quantum.ibm.com/) | Docs | Circuits, transpiler, runtime |
| [Qiskit Textbook (archived)](https://github.com/Qiskit/textbook) | Repo | Notebook-based reference |
| [PennyLane Codebook](https://pennylane.ai/codebook) | Interactive course | Hands-on gate and circuit exercises |
| [Cirq](https://quantumai.google/cirq) | Docs | Alternative framework from Google |
| [QuTiP Documentation](https://qutip.org/docs/latest/) | Docs | Open quantum systems simulation |

- [ ] Write a statevector simulator in NumPy supporting 1 and 2-qubit gates
- [ ] Verify your simulator against Qiskit on random circuits
- [ ] Run a circuit on a real device through IBM Quantum and compare with noiseless output

**Deliverables**
- [ ] `src/qsim/` simulator with tests against Qiskit
- [ ] `docs/noise_comparison.md` real hardware vs simulator

## Phase 3: Quantum Algorithms

Goal: Understand why each algorithm works, then implement it.

| Resource | Type | Why |
|----------|------|-----|
| [Quantum Computation and Quantum Information (Nielsen & Chuang)](https://www.cambridge.org/core/books/quantum-computation-and-quantum-information/01E10196D0A682A6AEFFEA52D53BE9AE) | Textbook | Standard reference, read selectively |
| [Quantum Algorithm Zoo](https://quantumalgorithmzoo.org/) | Catalog | Map of known algorithms and speedups |

- [ ] Deutsch-Jozsa, Bernstein-Vazirani, Simon
- [ ] Quantum Fourier transform and phase estimation
- [ ] Grover search with amplitude amplification analysis
- [ ] Shor's algorithm for factoring small numbers

**Deliverables**
- [ ] `src/algorithms/` with each algorithm and success-probability tests
- [ ] `docs/speedups.md` stating the actual speedup and its assumptions for each

## Phase 4: Variational & Quantum ML

Goal: Use near-term hardware ideas and judge them honestly.

| Resource | Type | Why |
|----------|------|-----|
| [PennyLane Demos](https://pennylane.ai/qml/demos) | Tutorials | VQE, QAOA, and quantum ML examples |
| [NIST Post-Quantum Cryptography](https://csrc.nist.gov/projects/post-quantum-cryptography) | Standards | What quantum computers mean for today's cryptography |

- [ ] VQE for the hydrogen molecule
- [ ] QAOA on a small Max-Cut instance
- [ ] Compare a quantum classifier with a classical baseline on the same data
- [ ] Read the NIST standards summary and list which of your Cybersecurity roadmap primitives are affected

**Deliverables**
- [ ] `notebooks/variational/` with VQE and QAOA results versus exact solutions
- [ ] `docs/qml_honest_evaluation.md` with classical baselines

## Phase 5: Error Correction & Hardware

Goal: Understand why scaling quantum computers is hard.

| Resource | Type | Why |
|----------|------|-----|
| [Stim](https://github.com/quantumlib/Stim) | Library | Fast stabilizer circuit simulation for error correction |
| [IBM Quantum Platform](https://quantum.cloud.ibm.com/) | Cloud access | Run on real hardware |

- [ ] Repetition code and the threshold idea
- [ ] Surface code basics and logical error rates in Stim
- [ ] Compare device noise across qubits and circuit depth

**Deliverables**
- [ ] `src/qec/` surface-code experiment in Stim with threshold plot
- [ ] `docs/hardware_limits.md` summarizing noise, depth limits, and scaling needs

## Capstone Projects

- [ ] Simulator: a NumPy statevector simulator verified against Qiskit, with a measured limit on qubit count
- [ ] Algorithms: Grover and a small Shor factoring run, with an honest analysis of speedup
- [ ] Applied: VQE for H2 compared with the exact answer and a classical method
- [ ] Error correction: a surface-code experiment showing logical error falling as code distance grows below threshold

## Repository Layout

```
quantum/
├── README.md
├── pyproject.toml
├── src/
│   ├── qsim/                 # your simulator
│   ├── algorithms/
│   └── qec/
├── notebooks/
│   ├── foundations/
│   └── variational/
├── tests/
└── docs/
    ├── noise_comparison.md
    ├── speedups.md
    ├── qml_honest_evaluation.md
    └── hardware_limits.md
```

## Engineering Rules

These are strict. A phase is not complete until its deliverables follow all of them.

### 1. Daily 1:3 Theory-to-Building Ratio

- [ ] For every 1 hour of reading or watching, spend 3 hours building, solving, or running labs
- [ ] Log hours in `docs/log.md` at the end of each session
- [ ] No new chapter until the previous one has working code or a written lab report

### 2. Git Branch Hygiene

- [ ] `main` is always green and never receives direct commits
- [ ] One branch per deliverable: `phase-N/short-description`
- [ ] Small commits with imperative messages; squash-merge via PR after checks pass
- [ ] Delete branches after merge

### 3. Quality Gates

- [ ] `mypy --strict src/`, `ruff`, and `pytest` pass
- [ ] Probabilistic outputs are tested with fixed seeds and statistical tolerances (`numpy.testing`)
- [ ] Every algorithm is checked against a classical or analytic reference
- [ ] Pin framework versions; quantum SDKs change APIs often

### 4. Branch-Specific Rules

- [ ] State the problem size and the classical baseline for every claimed speedup
- [ ] Report error bars and shots for any hardware result
- [ ] Do not call a result quantum advantage unless a stated, fair baseline was beaten
- [ ] Keep a changelog of SDK versions used for each notebook

## Exit Criteria

- [ ] Compute the outcome distribution of a small circuit by hand and match a simulator
- [ ] Explain why Grover is quadratic and Shor is superpolynomial, and what each requires
- [ ] Implement a small algorithm end to end on a simulator and a real device
- [ ] Explain what a post-quantum migration means for a real system
