# Quantum-Enhanced Conditional Molecular Generation

This repository contains the implementation and experimental results for the Master's Thesis: **"[Insert Your Thesis Title Here]"**.

The project implements a hybrid **Quantum-Classical Generative Model** designed to generate valid molecular strings (SELFIES) conditioned on specific chemical properties. It benchmarks various Quantum Ansatz strategies against classical autoregressive baselines (GRU).

## 🧪 Key Features

* **Hybrid Architecture:** Combines classical autoregressive conditioning (Attention/Hypernetworks) with a Variational Quantum Circuit (VQC) for state evolution.
* **Robust Molecular Representation:** Utilizes **SELFIES** to ensure surjectivity and robustness, guaranteeing that 100% of generated outputs correspond to valid molecular graphs.
* **Novel Conditioning Mechanism:** Implements a geometrically optimized **Data Re-uploading** strategy using `CRX` gates to maximize gradient sensitivity and expressivity.
* **Environment-Assisted Evolution:** Utilizes ancillary "environment" qubits in the Hamiltonian evolution to mediate long-range correlations between token features.

## 🧠 Architecture Overview

The model operates as an autoregressive sequence generator. At each step , the history and target properties are processed to evolve a quantum state , which is measured to sample the next token.

### The Quantum Ansatz

The core innovation lies in the Variational Quantum Circuit (VQC) design, selected via extensive ablation studies:

1. **Conditional Injection:** We employ `CRX` gates (Controlled-Rotation X) rather than `CRZ`.
* **Why?** `CRX` induces orthogonal rotation relative to the computational basis (Z-axis), ensuring immediate probability modulation and non-linear mixing with the property context ().


2. **Hamiltonian Evolution:** Layers conclude with a Time-Evolution operator under a diagonal Hamiltonian () extended to include **Environment Qubits**.
3. **Data Re-uploading:** Property information is re-injected at every layer depth  to preserve signal against unitary scrambling.

### Benchmark Models

* **AAQC (Global Context):** Uses causal attention to summarize history for the quantum circuit.
* **SWQH (Local Context):** Uses a Sliding Window Hypernetwork to modulate circuit parameters.
* **Classical Baseline:** A conditional GRU network with input injection ().

## 📊 Performance & Results

We benchmarked the architectures on **[Insert Dataset Name, e.g., QM9/ZINC]**. Training was performed via **ideal state-vector simulation** to isolate theoretical expressivity from hardware noise.

### 1. Architecture Selection (Ablation)

Comparison of injection strategies (Single vs. Re-uploading) and Hamiltonian scope (Token vs. Token+Env).

<p align="center">
<img src="images/quantum_architecture_convergence_12x6.png" width="600" alt="Architecture Convergence">
</p>

*Result: The configuration combining Data Re-uploading with Environment Qubits (Orange) achieves the lowest validation loss and fastest convergence.*

### 2. Capacity Sweep (Depth vs. Ancillas)

<p align="center">
<img src="images/quantum_capacity_sweep_convergence.png" width="600" alt="Capacity Sweep">
</p>

*Result: Increasing circuit depth () and adding ancillary qubits consistently improves density estimation performance.*
