from qiskit import QuantumCircuit, transpile
from qiskit_aer import AerSimulator
from qiskit.visualization import plot_histogram

# Initialize the simulator (used for all tasks)
simulator = AerSimulator()

# --- Task 1: Change shots to 100 (using the original 1-qubit circuit) ---
print("--- Task 1: 1 Qubit, 100 Shots ---")
qc_task1 = QuantumCircuit(1, 1)
qc_task1.h(0)
qc_task1.measure(0, 0)

job_task1 = simulator.run(transpile(qc_task1, simulator), shots=100) # CHANGED SHOTS
counts_task1 = job_task1.result().get_counts()
print("Counts:", counts_task1)
plot_histogram(counts_task1)
# Note: You'll see counts for '0' and '1' closer to 50/50.

# --- Task 2: Add a second qubit with Hadamard on both ---
print("\n--- Task 2: 2 Qubits, Hadamard on Both ---")
qc_task2 = QuantumCircuit(2, 2) # 2 qubits, 2 classical bits
qc_task2.h(0)
qc_task2.h(1) # Hadamard on Qubit 1
qc_task2.measure(0, 0)
qc_task2.measure(1, 1) # Measure Qubit 1 into classical bit 1

job_task2 = simulator.run(transpile(qc_task2, simulator), shots=100)
counts_task2 = job_task2.result().get_counts()
print("Counts:", counts_task2)
plot_histogram(counts_task2)
# Note: You'll see counts for '00', '01', '10', and '11' (four possible outcomes).

# --- Task 3: Replace Hadamard with X gate (on a 1-qubit circuit) ---
print("\n--- Task 3: 1 Qubit, X Gate ---")
qc_task3 = QuantumCircuit(1, 1)
qc_task3.x(0) # Replaced qc.h(0) with qc.x(0)
qc_task3.measure(0, 0)

job_task3 = simulator.run(transpile(qc_task3, simulator), shots=100)
counts_task3 = job_task3.result().get_counts()
print("Counts:", counts_task3)
plot_histogram(counts_task3)
# Note: You will see 100% of the counts for '1'.
