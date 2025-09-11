# QuantumSimulatorValidator

This repository is a public version of the [QuantumSimulatorValidator](https://github.com/vili-1/QuantumSimulatorValidator) project, which is actively under development.


### Publications

Klimis, V., Bensoussan, A., Chachkarova, E., Even-Mendoza, K., Fortz, S., & Lenihan, C. (Accepted/In press). Shaking Up Quantum Simulators with Fuzzing and Rigour. In ACM SIGPLAN International Conference on Object-Oriented Programming Systems, Languages, and Applications (OOPSLA): OOPSLA 2025 Article 322 https://doi.org/10.1145/3763100
```
@inbook{OOPSLA:FuzzQ:2025,
   title = "Shaking Up Quantum Simulators with Fuzzing and Rigour",
   abstract = "Quantum computing platforms rely on simulators for modelling circuit behaviour prior to hardware execution, where inconsistencies can lead to costly errors. While existing formal validation methods typically target specific compiler components to manage state explosion, they often miss critical bugs. Meanwhile, conventional testing lacks systematic exploration of corner cases and realistic execution scenarios, resulting in both false positives and negatives.We present FuzzQ, a novel framework that bridges this gap by combining formal methods with structured test generation and fuzzing for quantum simulators. Our approach employs differential benchmarking complemented by mutation testing and invariant checking. At its core, FuzzQ utilises our Alloy-based formal model of QASM 3.0, which encodes the semantics of quantum circuits to enable automated analysis and to generate structurally diverse, constraint-guided quantum circuits with guaranteed properties. We introduce several test oracles to assess both Alloy{\textquoteright}s modelling of QASM 3.0 and simulator correctness, including invariant-based checks, statistical distribution tests, and a novel cross-simulator unitary consistency check that verifies functional equivalence modulo global phase, revealing discrepancies that standard statevector comparisons fail to detect in cross-platform differential testing.We evaluate FuzzQ on both Qiskit and Cirq, demonstrating its platform-agnostic effectiveness. By executing over 800,000 quantum circuits to completion, we assess throughput, code and circuit coverage, and simulator performance metrics, including sensitivity, correctness, and memory overhead. Our analysis revealed eight simulator bugs, six previously undocumented. We also outline a path for extending the framework to support mixed-state simulations under realistic noise models.",
   keywords = "Quantum Computing, Alloy, Verification/Validation,, est Case Generation, Fuzzing",
   author = "Vasileios Klimis and Avner Bensoussan and Elena Chachkarova and Karine Even-Mendoza and Sophie Fortz and Connor Lenihan",
   note = "After the first author, the rest of the authors are listed in alphabetical order.",
   year = "2025",
   month = aug,
   day = "13",
   doi = "10.1145/3763100",
   language = "English",
   booktitle = "ACM SIGPLAN International Conference on Object-Oriented Programming Systems, Languages, and Applications (OOPSLA)",
}
```

Klimis, V., Bensoussan, A., CHACHKAROVA, E., Even Mendoza, K., Fortz, S., & Lenihan, C. (2025). FuzzQ Artifact: Shaking Up Quantum Simulators with Fuzzing and Rigour [Data set]. Zenodo. https://doi.org/10.5281/zenodo.16918102
```
@dataset{klimis_2025_16918102,
  author       = {Klimis, Vasileios and
                  Bensoussan, Avner and
                  CHACHKAROVA, ELENA and
                  Even Mendoza, Karine and
                  Fortz, Sophie and
                  Lenihan, Connor},
  title        = {FuzzQ Artifact: Shaking Up Quantum Simulators with
                   Fuzzing and Rigour
                  },
  month        = aug,
  year         = 2025,
  publisher    = {Zenodo},
  doi          = {10.5281/zenodo.16918102},
  url          = {https://doi.org/10.5281/zenodo.16918102},
}
```

### Project Overview

This project aims to evaluate the performance, correctness, and precision of quantum simulators implemented on various Python-based platforms. The validation involves:

- **Fuzzing and Test Case Generation**: Using a fuzzing platform to generate diverse simulation scenarios.
- **Cross-Platform Testing**: Testing scenarios across different computational environments (e.g., x86 vs. ARM architectures, and Python builds with various C/C++ compilers).
- **Comparison with Quantum Hardware**: Assessing the alignment of simulated quantum behaviour with real quantum devices to highlight discrepancies or confirm the accuracy of quantum simulators against near-term intermediate-scale quantum (NISQ) hardware.


### Modelling Quantum Circuits

A key aspect of validation is the formalisation of quantum circuits, which enables systematic exploration of simulation outcomes and enhances the reliability of results. This process encompasses several important components:

- **Mathematical Modelling**: We utilise formal methods to create precise mathematical representations of quantum circuits. This ensures a rigorous framework for both analysis and validation, allowing for the verification of circuit properties and performance metrics.

- **Specification Languages**: Through the specification language we define circuit properties and constraints in a structured manner. This facilitates systematic exploration and verification of circuit behaviour, enabling us to rigorously assess compliance with desired characteristics.

- **Simulation of Quantum Behaviour**: We develop advanced simulations that accurately reflect the theoretical behaviour of quantum circuits. These simulations serve as benchmarks against which results from real quantum hardware can be compared, allowing for a thorough evaluation of the fidelity and accuracy of quantum simulators.

Through these methods, we aim to establish a comprehensive framework for formalising quantum circuits, contributing to the robustness of simulation results and the overall validation process.


### Team

**Queen Mary University of London (School of Electronic Engineering and Computer Science):**

- Vasileios Klimis

**King's College London (Informatics Department):**

- Avner Bensoussan
- Karine Even-Mendoza
- Sophie Fortz

**King's College London (Physics Department):**

- Elena Chachkarova
- Connor Lenihan


### Seed Generation

This section focuses on generating Quantum Circuits (QC) automatically by defining and applying specific properties as input constraints. This approach allows for the systematic creation of test cases that examine specific behaviours and configurations in quantum circuits, serving both for validation of simulation platforms and exploration of particular quantum properties.

#### Example Properties and Constraints

The automatic generation can be driven by properties that represent typical or challenging scenarios in quantum computing. Below are examples of properties we may define to generate circuits with desired characteristics:


1. **Balanced Superposition**: Circuits where qubits are initialized to a balanced superposition state. This may involve applying `H` gates to all qubits.
   - **Generated Circuit**: `H` on each qubit in a three-qubit circuit.

2. **Reversible Circuits**: Circuits where a sequence of operations can be undone by applying the same gates in reverse order.
   - **Generated Circuit**: Apply `H` on `q_0`, `CX` between `q_0` and `q_1`, then `CX` and `H` in reverse order.



#### Example Output

Given these properties, an automatically generated circuit might look as follows:

<pre>
        
q_0: ──H──────■──────■─────X─────X─────H───
              │      │     │     │
q_1: ──H──────X──────┼─────■─────┼─────H───
                     │           │
q_2: ──H─────────────X───────────■─────H───

</pre>

#### Explanation of the Circuit

1. **Balanced Superposition**: Each of the three qubits starts in the |0⟩ state and is transformed into a balanced superposition of |0⟩ and |1⟩ states by applying Hadamard gates.
2. **Reversible Operations**: The CNOT gates create entanglement between the qubits. Each CNOT gate is reversible, and applying them in reverse order will return the qubits to their original states.
3. **Final State**: The Hadamard gates are applied again to reverse the superposition state back to the initial |0⟩ state.



### Testing Simulators

The following quantum (higher-level) simulators are considered for testing:

- **Qiskit** (IBM)
- **Braket** (AWS)
- **Cirq** (Google)
- **Tket**

Note: Other related frameworks: OpenQASM (low-level).
 

### Hardware Specifications

- Architectures: x86, ARM
