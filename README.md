# Quantum-Enhanced Conditional Molecular Generation

This repository contains the implementation and experimental results for the Master's Thesis: **Variational Quantum Autoregressive Models for Conditional
Molecular Generation** by Esther Gallego Estevez.

The project implements a hybrid **Quantum-Classical Generative Model** designed to generate valid molecular strings (SELFIES) conditioned on specific chemical properties. It benchmarks various Quantum Ansatz strategies against classical autoregressive baselines (GRU).

## 🧪 Key Features

* **Hybrid Architecture:** Combines classical autoregressive conditioning (Attention/Hypernetworks) with a Variational Quantum Circuit (VQC) for state evolution.
* **Robust Molecular Representation:** Utilizes **SELFIES** to ensure surjectivity and robustness, guaranteeing that 100% of generated outputs correspond to valid molecular graphs.
* **Novel Conditioning Mechanism:** Implements a geometrically optimized **Data Re-uploading** strategy using `CRX` gates to maximize gradient sensitivity and expressivity.
* **Environment-Assisted Evolution:** Utilizes ancillary "environment" qubits in the Hamiltonian evolution to mediate long-range correlations between token features.

## 🧠 Architecture Overview

The model operates as an autoregressive sequence generator. At each step , the history and target properties are processed to evolve a quantum state , which is measured to sample the next token.

<img width="603" height="377" alt="image" src="https://github.com/user-attachments/assets/9954da42-f22a-411d-b49d-b44bc584dd99" />


### The Quantum Ansatz

The core innovation lies in the Variational Quantum Circuit (VQC) design, selected via extensive ablation studies:

1. **Conditional Injection:** We employ `CRX` gates (to condition the molecular properties into the token qubits).
2. **Hamiltonian Evolution:** Layers conclude with a Time-Evolution operator under a diagonal Hamiltonian, extended to include **Environment Qubits**.
3. **Data Re-uploading:** Property information is re-injected at every layer depth  to preserve signal against unitary scrambling.

<img width="1049" height="475" alt="image" src="https://github.com/user-attachments/assets/3fa1fd6a-eba9-48d3-adf3-7639e060651a" />


### Benchmark Models

* **AAQC (Global Context):** Uses causal attention to summarize history for the quantum circuit.
* **SWQH (Local Context):** Uses a Sliding Window Hypernetwork to modulate circuit parameters.
* **Classical Baseline:** A conditional GRU network with input injection ().

## 📊 Performance & Results

We benchmarked the architectures on ChEMBL. Training was performed via **ideal state-vector simulation** to isolate theoretical expressivity from hardware noise.

<img width="765" height="584" alt="image" src="https://github.com/user-attachments/assets/1adc940d-e87c-49d0-953e-a146fed4aa40" />



