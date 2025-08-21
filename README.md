# Classical vs Quantum Machine Learning on the Heart Disease Dataset  

## Project Overview  
This project explores the comparison between **classical machine learning (ML)** and **quantum machine learning (QML)** using the [UCI Heart Disease dataset](https://www.kaggle.com/ronitf/heart-disease-uci).  

The work was carried out as part of the **COMP47950 – Quantum Machine Learning** module at University College Dublin. The core idea was to benchmark a classical model against quantum-inspired approaches, first in simulation and then on a real quantum computer hosted by IBM.  

---

## Motivation  
Quantum computing promises speedups in certain computational tasks due to quantum phenomena like **superposition** and **entanglement**. One of the most exciting potential applications is in **machine learning**. However, today’s quantum hardware is still in the **NISQ (Noisy Intermediate-Scale Quantum)** era, meaning devices are error-prone and resource-limited.  

This project investigates:  
- How a **classical model** (Random Forest) performs on the dataset.  
- How different **variational quantum circuits** perform when simulated.  
- How the **best quantum circuit** performs when run on a **real IBM Quantum device**.  

The goal is not only accuracy, but also **runtime performance, feasibility, and noise sensitivity**.  

---

## Methods  
1. **Classical Approach**  
   - Implemented a **Random Forest Classifier** using scikit-learn.  
   - Provides a strong, fast baseline for heart disease classification.  

2. **Quantum Approach (Simulation)**  
   - Implemented multiple **variational quantum circuits (VQCs)** in **PennyLane**.  
   - Explored different circuit depths, qubit counts, and ansatz designs.  
   - Simulated on a classical backend for training and evaluation.  

3. **Quantum Approach (Real Hardware)**  
   - The **best-performing simulated circuit** was executed on an **IBM Quantum backend**.  
   - Results were compared with simulation and the classical model to illustrate the effect of hardware noise and queue times.  

---

## Results & Findings  

### Classical Random Forest  
- **Training & inference:** Completed in **seconds**.  
- **Performance:** Stable and high accuracy, with no major computational overhead.  

### Quantum Simulation (PennyLane)  
- **Training time:** Took **hours** to train circuits due to exponential scaling with qubits and gates.  
- **Performance:** Varied depending on the ansatz, with some circuits approaching the classical baseline but generally less stable.  
- **Insights:** Circuit design (“ansatz lottery”) had a huge impact on results.  

### Quantum Hardware (IBM Quantum)  
- **Execution time:** Jobs sat in a queue and took **hours** to complete.  
- **Performance:** Significantly degraded compared to simulation due to **noise** and **limited qubit fidelity**.  
- **Insight:** Real hardware highlights the limitations of current NISQ devices for practical ML tasks.  

### Overall Comparison  

| Approach                | Training / Execution Time | Performance | Notes | Accuracy |
|--------------------------|---------------------------|-------------|-------|--------|
| **Random Forest (Classical)** | Seconds                   | High accuracy, stable | Fast and reliable baseline | ~85% |
| **Quantum Simulation**   | Hours                     | Moderate, varied | Strongly depends on ansatz design | ~83% |
| **Quantum Hardware**     | Hours (including queue)   | Moderate, noisy results | Performance degraded due to hardware noise | ~78% |

---

## Key Takeaways  
- Classical ML is currently **far more efficient and effective** for this type of structured dataset.  
- QML remains experimental but offers an important learning opportunity to understand the challenges of designing quantum circuits.  
- The project demonstrates the **gap between theoretical promise and practical limitations** in today’s quantum hardware.  
- Running QML on a real device is valuable for experience, but highlights why quantum advantage is still a research goal rather than reality (Except for specific fields like cryptography).
- Shallower (fewer gates) and shorter (fewer qubits) circuits trained faster and generally performed better. More than 2 qubits and a moderate circuit depth will find diminishing returns very quickly. However, a tiny circuit also does not have enough expressivity to realise the data. 
- The custom VQC I implemented in Pennylane only worked if temperature was added, which gives the parametrised gates a much-needed boost.
- Pennylane is harder to implement that Qiskit

---

## References  
- [PennyLane](https://pennylane.ai/) – Framework for quantum machine learning  
- [IBM Quantum](https://quantum-computing.ibm.com/) – Cloud-based access to quantum devices  
- [Heart Disease Dataset (Kaggle)](https://www.kaggle.com/ronitf/heart-disease-uci)  
