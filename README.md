# Project: Improving Quantum Reservoir Computing with Entangled Reservoirs

This project addresses the challenge of using a hybrid classical & quantum approach for Reservoir Computing, a topic presented in this repository. We demonstrate a significant performance improvement over the initial baseline by introducing an advanced, entangled multi-reservoir architecture.

---

## 1. The Challenge: Aperiodic Time-Series Prediction

The core challenge is to accurately predict the future evolution of a complex, aperiodic, and noisy time-series. The specific task uses a signal generated from the superposition of two damped harmonic oscillators with irrational frequency ratios, making it difficult for simple models to capture its dynamics.

The baseline for this work is established in `Classical-Quantum-Reservoir-Computing.ipynb`. That notebook explores several Quantum Reservoir Computing (QRC) models and finds that a **hybrid classical-quantum model** provides the best performance, achieving an **R² score of 0.595**.

This initial finding suggests that combining different types of computational dynamics is beneficial. However, the quantum part of that model consists of multiple *independent* reservoirs, which may not fully exploit the potential of quantum computation.

## 2. Our Solution: Entangled Multi-Reservoir Architecture

To improve upon the baseline, we hypothesized that the model's predictive power could be enhanced by creating correlations between the individual quantum reservoirs.

The work in `penny_oqrc.ipynb` investigates this hypothesis by implementing and comparing three distinct multi-reservoir architectures using the PennyLane framework:

1.  **Independent Reservoirs:** Each quantum reservoir evolves independently. This serves as a like-for-like comparison with the quantum part of the baseline model.

2.  **Channel Coupling:** The reservoirs evolve independently, but their output measurement results (observables) are classically mixed together before being fed to the final readout layer.

3.  **Entangled Coupling:** The reservoirs are combined into a single, larger quantum circuit. CNOT gates are introduced *between* the reservoirs, allowing them to become entangled during their evolution. This enables the system to develop and leverage quantum correlations across all reservoirs, creating a richer, more expressive feature space.

## 3. Theoretical Justification and Related Work

Our approach is directly supported by a growing body of academic research indicating that entanglement is a key resource for enhancing the power of QRCs.

- **K. Fujii and K. Nakajima (2017)**, in "Harnessing entanglement in quantum reservoir computing" (arXiv:1607.03954), established that entanglement within a reservoir is crucial for its computational capability. They showed that the memory capacity of a QRC is directly related to the degree of entanglement, providing a strong theoretical foundation for our hypothesis.

- **S. Dasgupta, et al. (2023)**, in "The role of entanglement and interference in quantum reservoir computing" (arXiv:2301.09619), further explored this, finding that entanglement between different parts of a reservoir allows it to access a much larger and more complex feature space. This aligns with our finding that an entangled system outperforms classically-coupled or independent systems.

- The concept of using coupled quantum systems for scalability and performance is also well-documented. For instance, **M. A. Negoro, et al. (2018)** demonstrated that a system of two coherently coupled quantum oscillators could achieve high accuracy on benchmark tasks (Nature Communications, s41467-018-05678-x), reinforcing the idea that inter-system correlations are a powerful resource.

This research confirms that our strategy of entangling reservoirs is a promising and theoretically sound path toward more powerful QRC models.

## 4. Findings and Improvement

Our experimental results clearly demonstrate the superiority of the entangled architecture, validating the principles from the cited research.

| Model Architecture | Framework | R² Score |
| :--- | :--- | :--- |
| Classical-Only (Baseline) | Qiskit | 0.063 |
| Quantum-Only (Independent) | Qiskit | 0.371 |
| **Hybrid Classical-Quantum (Baseline)** | **Qiskit** | **0.595** |
| --- | --- | --- |
| Independent Reservoirs | PennyLane | 0.465 |
| Channel Coupled Reservoirs | PennyLane | 0.608 |
| **Entangled Reservoirs (Our Solution)** | **PennyLane** | **0.672** |

### Conclusion

Our investigation yielded two key insights:

1.  **Confirmation of Baseline:** The "Channel Coupling" method, which classically mixes information, performed on par with the hybrid classical-quantum model (R² ≈ 0.608 vs. 0.595). This suggests that simply adding more information streams (whether from a classical reservoir or another quantum one) gives a similar, moderate performance boost.

2.  **Superiority of Entanglement:** The **Entangled Reservoir model achieved a final R² score of 0.672**, a significant improvement over all other tested architectures. This finding strongly suggests that enabling quantum correlations between reservoirs allows the system to capture more complex and subtle temporal features within the data, a result that is well-aligned with the foundational research in the field.

In summary, for this time-series prediction challenge, **entangling quantum reservoirs is a more effective strategy for improving performance** than simply combining independent quantum and classical systems.