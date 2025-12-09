# HHL Algorithm Benchmarking Suite

## Overview

This repository contains a comprehensive benchmarking suite for the HHL (Harrow-Hassidim-Lloyd) quantum algorithm, implementing the paper **"Towards provably efficient quantum algorithms for large-scale machine learning models"**.

The notebook compares state-of-the-art HHL implementations across multiple quantum computing frameworks with realistic performance metrics.

## Features

### 1. **Multi-Framework Implementation**
- **Qiskit (IBM Quantum)**: Production-ready implementation with hardware support
- **PennyLane (Xanadu)**: Hybrid quantum-classical ML workflows
- **Classical Baseline**: NumPy-based solver for comparison

### 2. **State Tomography Techniques**
- **Maximum Likelihood Estimation (MLE)**: Optimal for high-fidelity reconstruction
- **Compressed Sensing**: Efficient for low-rank quantum states
- **Direct Fidelity Estimation (DFE)**: Fast benchmarking tool

### 3. **Comprehensive Benchmarking Metrics**
- Runtime comparison across frameworks
- Accuracy measurements (error and fidelity)
- Resource requirements (qubits, gates, circuit depth)
- Scalability analysis for different problem sizes

### 4. **Machine Learning Applications**
- Ridge regression using HHL
- Linear systems solving
- Support for quantum-enhanced ML workflows

## Installation

### Prerequisites
- Python 3.8 or higher
- pip package manager

### Setup

```bash
# Clone the repository
git clone https://github.com/dieser-max-tum/dieser-max-tum.github.io.git
cd dieser-max-tum.github.io

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter Lab
jupyter lab hhl_algorithm_benchmarking.ipynb
```

### Alternative: Virtual Environment

```bash
# Create virtual environment
python -m venv hhl_env
source hhl_env/bin/activate  # On Windows: hhl_env\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Launch notebook
jupyter lab hhl_algorithm_benchmarking.ipynb
```

## Usage

### Quick Start

1. **Open the notebook**: `hhl_algorithm_benchmarking.ipynb`
2. **Run all cells**: Select "Run > Run All Cells" in Jupyter Lab
3. **Review results**: Check generated visualizations and CSV files

### Customization

#### Adjust Problem Sizes
```python
# In Section 7: Run Benchmarks
problem_sizes = [2, 4, 8]  # Modify this list
```

#### Change Test Conditions
```python
# In Section 6: Benchmarking Framework
A, b = benchmark.generate_test_problem(
    size=4, 
    condition_number=20  # Adjust conditioning
)
```

#### Add Custom Implementations
```python
# Create your own solver class
class CustomHHLSolver:
    def __init__(self, matrix, vector):
        self.matrix = matrix
        self.vector = vector
        self.runtime = 0
    
    def solve(self):
        # Your implementation
        pass
    
    def get_solution_vector(self):
        return self.result
```

## Benchmarking Results

The notebook generates several output files:

1. **hhl_benchmark_results.csv**: Detailed numerical results
2. **hhl_benchmark_report.txt**: Summary statistics report
3. **hhl_benchmark_results.png**: Comparative visualizations
4. **hhl_scalability.png**: Resource scaling analysis

### Expected Performance

For a 2x2 matrix:
- **Classical Solver**: ~0.0001s
- **Qiskit HHL**: ~0.1-1s (simulator)
- **PennyLane HHL**: ~0.1-1s (simulator)

*Note: Quantum implementations show advantage for larger, well-structured matrices*

## Understanding HHL Algorithm

### What is HHL?

The HHL algorithm solves linear systems Ax = b exponentially faster than classical algorithms under certain conditions:

- **Input**: Hermitian matrix A, vector b
- **Output**: Quantum state |x⟩ proportional to solution x
- **Complexity**: O(log(N) s²κ²/ε) vs O(N s κ) classical
  - N: matrix dimension
  - s: sparsity
  - κ: condition number
  - ε: precision

### Key Requirements

1. **Matrix Properties**:
   - Hermitian (or can be made Hermitian)
   - Well-conditioned (κ < 100 preferred)
   - Sparse structure helps

2. **Quantum Resources**:
   - O(log N) qubits for N×N matrix
   - Additional ancilla qubits
   - Quantum RAM (QRAM) for large problems

3. **Limitations**:
   - Output is quantum state (needs tomography for classical data)
   - Requires amplitude amplification for efficiency
   - NISQ devices have ~100 qubits (limits to ~2^50 dimensional problems theoretically)

## State Tomography Selection Guide

### When to Use Each Method

| Method | Best For | Measurements | Complexity | Accuracy |
|--------|----------|--------------|------------|----------|
| **MLE** | High-fidelity reconstruction | O(d²) | O(d⁶) | Highest |
| **Compressed Sensing** | Large low-rank states | O(d log d) | O(d³) | High |
| **Direct Fidelity** | Quick validation | O(1/ε²) | O(d) | N/A (fidelity only) |

### Recommendations

- **For benchmarking**: Start with Direct Fidelity Estimation
- **For verification**: Use MLE with sufficient measurements
- **For large systems**: Try Compressed Sensing if state is low-rank

## Performance Optimization Tips

### 1. Matrix Conditioning
```python
# Check condition number
condition_num = np.linalg.cond(A)
print(f"Condition number: {condition_num}")

# Precondition if needed
if condition_num > 100:
    # Apply preconditioning
    D = np.diag(1 / np.sqrt(np.diag(A)))
    A_precond = D @ A @ D
```

### 2. Problem Size Selection
- Start with 2×2, 4×4 for testing
- Gradually increase to 8×8, 16×16
- Monitor qubit requirements: ~log₂(N) + 3

### 3. Framework Selection
- **Research/Prototyping**: PennyLane (easier debugging)
- **Production/Hardware**: Qiskit (mature ecosystem)
- **Hybrid ML**: PennyLane (better PyTorch/TF integration)

## Machine Learning Applications

### Ridge Regression Example

```python
# Generate ML problem
from sklearn.datasets import make_regression
X, y = make_regression(n_samples=100, n_features=10)

# Form ridge regression system
lambda_reg = 0.1
A = X.T @ X + lambda_reg * np.eye(X.shape[1])
b = X.T @ y

# Solve with HHL
solver = QiskitHHL(A, b)
solution = solver.solve()
```

### Other Applications
- Support Vector Machines (kernel evaluation)
- Principal Component Analysis
- Recommendation systems
- Portfolio optimization

## GitHub Repositories

### Recommended Resources

1. **Qiskit Machine Learning**
   - https://github.com/Qiskit/qiskit-machine-learning
   - IBM's quantum ML library

2. **PennyLane**
   - https://github.com/PennyLaneAI/pennylane
   - Xanadu's differentiable quantum computing

3. **Quantum Algorithms**
   - Search GitHub for "HHL algorithm quantum"
   - Various implementations and tutorials

4. **QuTiP**
   - https://github.com/qutip/qutip
   - Quantum Toolbox in Python

## Troubleshooting

### Common Issues

#### 1. Import Errors
```bash
# Ensure all packages are installed
pip install --upgrade qiskit qiskit-aer qiskit-algorithms pennylane
```

#### 2. Memory Issues
```python
# Reduce problem size
problem_sizes = [2, 4]  # Instead of [2, 4, 8, 16]
```

#### 3. Slow Execution
```python
# Use fewer iterations
n_trials = 1  # Instead of multiple trials
```

#### 4. Convergence Problems
```python
# Check matrix conditioning
condition_num = np.linalg.cond(matrix)
if condition_num > 100:
    print("Warning: Matrix is ill-conditioned")
```

## Contributing

Contributions are welcome! Please feel free to:
1. Add new HHL implementations
2. Improve tomography methods
3. Add more ML applications
4. Optimize performance
5. Fix bugs

## References

### Key Papers

1. **Original HHL Algorithm**
   - Harrow, A. W., Hassidim, A., & Lloyd, S. (2009). "Quantum algorithm for linear systems of equations." Physical Review Letters, 103(15), 150502.

2. **Quantum Machine Learning**
   - Biamonte, J., et al. (2017). "Quantum machine learning." Nature, 549(7671), 195-202.

3. **State Tomography**
   - Gross, D., et al. (2010). "Quantum state tomography via compressed sensing." Physical Review Letters, 105(15), 150401.

### Online Resources

- Qiskit Textbook: https://qiskit.org/textbook
- PennyLane Demos: https://pennylane.ai/qml/demonstrations.html
- Quantum Algorithm Zoo: https://quantumalgorithmzoo.org/

## License

This project is open source and available under the MIT License.

## Contact

For questions or issues, please open an issue on GitHub or contact the repository maintainer.

## Acknowledgments

- IBM Quantum for Qiskit framework
- Xanadu for PennyLane framework
- Quantum computing research community

---

**Note**: This benchmarking suite is designed for educational and research purposes. For production quantum computing applications, please consult with quantum computing experts and consider the limitations of current NISQ devices.
