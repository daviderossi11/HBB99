# HBB99 Quantum Secret Sharing & Attack Analysis

This repository contains the implementation and security analysis of the HBB99 Quantum Secret Sharing (QSS) protocol[cite: 2]. Developed by Davide Rossi and Alberto Ovena as part of the MSc in Cybersecurity Engineering program at Politecnico di Torino[cite: 2]. 

The project focuses on establishing a correlated bit string for Key Distribution using multiparticle entanglement (GHZ states)[cite: 2]. We implemented the standard protocol, executed active insider attacks to compromise it, and developed a structural fix to secure the exchange[cite: 2].

**All code implementations and interactive demonstrations are located in `HBB99_Demos.ipynb`.** You can run this notebook directly in Google Colab or your preferred Jupyter environment.

## Hardware Execution
The protocol and its associated attacks were implemented and executed on **Lagrange**, an IQM superconducting quantum computer available at Politecnico di Torino[cite: 2]. Due to the noisy nature of this NISQ processor, we mitigated readout noise by selecting the measurement of the run with the highest count, reducing the baseline error to near-zero[cite: 2].

## Vulnerability Analysis & Implemented Attacks
We demonstrated that the standard HBB99 protocol is vulnerable to a dishonest participant (an insider attack) who exploits the order of basis announcements[cite: 2]. We implemented three distinct attack vectors within the notebook:

*   **Intercept-Resend Attack:** A naive approach where the malicious insider (Charlie) measures the GHZ particles in a random basis and resends a fresh particle to the victim[cite: 2]. This attack proved highly detectable, causing the protocol to abort[cite: 2].
*   **Fake Entanglement Attack:** A sophisticated attack where the insider uses two additional qubits to create a fake Bell pair[cite: 2]. By delaying measurement until the other bases are announced, the attacker successfully reconstructs the secret key without triggering the error threshold[cite: 2].
*   **Ancilla Attack:** The attacker forces an ancilla qubit to interact with the received particles[cite: 2]. By waiting to discover the other parties' measurement bases, the attacker perfectly distinguishes the mixed states, avoiding detection and fully compromising the security of the key[cite: 2].

## The Fairness Fix: Commit-then-Reveal
To patch the vulnerabilities exposed by the Fake Entanglement and Ancilla attacks, we implemented a **Commit-then-Reveal** mechanism[cite: 2]. 

The root vulnerability of the standard protocol is "delayed choice"—allowing the attacker to capture the system but wait for the disclosure of measurement bases before acting[cite: 2]. Our fix enforces a strict ordering during test rounds: all participants must first commit and announce their outcome bits before any measurement bases are revealed[cite: 2]. This forces the attacker to guess the target parity blindly, transforming deterministic cheating into a probabilistic gamble and successfully securing the protocol[cite: 2].

## Detailed Documentation
**For a complete deep dive into the quantum theory, mathematical proofs, circuit architectures, and our methodology, please view the attached `HBB99.pdf` presentation.**[cite: 2]
