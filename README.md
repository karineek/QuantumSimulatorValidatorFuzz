# QuantumSimulatorValidator

This is a visible repository of the [QuantumSimulatorValidator](https://github.com/vili-1/QuantumSimulatorValidator), which is currently under development.

In this project, we are using fuzzing/test-case generation platform to examine the performance, correctness and precision of quantum simulation via various Python platforms, and later compare these data against Qunatum hardware (with experiments being done on real quantum computing devices on the other hand) to test the correctness of various Python-based quantum simulators vs quantum hardware (NISQ).


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
