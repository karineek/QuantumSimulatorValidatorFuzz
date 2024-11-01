# QuantumSimulatorValidator

This is a visible repository of the [QuantumSimulatorValidator](https://github.com/vili-1/QuantumSimulatorValidator), which is currently under development.

In this project, we are using fuzzing/test-case generation platform to examine the performance, correctness and precision of quantum simulation via various Python platforms (with many of the tests being checked classically, say X86 vs ARM or building Python systems using different C/C++ compilers), and later compare these data against Qunatum hardware (with experiments being done on real quantum computing devices on the other hand) to test the correctness of various Python-based quantum simulators vs quantum hardware (NISQ).

#### TEAM

- (QMUL/School of Electronic Engineering and Computer Science): Vasileios Klimis
- (KCL/Informatics Department): Avner Bensoussan, Karine Even-Mendoza, Sophie Fortz
- (KCL/Physics Department): Elena Chachkarova, Connor Lenihan

## Seeds Generation

We aim to develop a method for generating QC automatically based on various properties (as input).

#### Example Output

After running the quantum circuit with Qiskit, you may get a result like this:

<pre>
                                               ┌───┐ ░ ┌─┐         
   q_0: ────────────────────────────────■──────┤ X ├─░─┤M├─────────
           ┌────────┐                   │      └─┬─┘ ░ └╥┘┌─┐      
   q_1: ───┤ Rx(15) ├───────────────────┼────────■───░──╫─┤M├──────
        ┌──┴────────┴─┐┌──────────────┐ │        │   ░  ║ └╥┘┌─┐   
   q_2: ┤ U(15,15,15) ├┤ U(π/2,15,15) ├─┼────────■───░──╫──╫─┤M├───
        └┬───────────┬┘└──────────────┘ │P(15)       ░  ║  ║ └╥┘┌─┐
   q_3: ─┤ U(0,0,15) ├──────────────────■────────────░──╫──╫──╫─┤M├
         └───────────┘                               ░  ║  ║  ║ └╥┘
meas: 4/════════════════════════════════════════════════╩══╩══╩══╩═
                                                        0  1  2  3

Result: {'0000': 58, '0010': 429, '0100': 61, '0111': 476}
</pre>

## Testing Simulators

We consider the following systems:
- qiskit
- braket
- cirq
- tket

Hardware specification: X86, ARM.
