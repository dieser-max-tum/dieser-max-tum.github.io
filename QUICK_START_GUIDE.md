# HHL Algorithm Benchmarking - Quick Start Guide

## 🚀 Get Started in 5 Minutes

### 1. Installation (2 minutes)

```bash
# Clone the repository
git clone https://github.com/dieser-max-tum/dieser-max-tum.github.io.git
cd dieser-max-tum.github.io

# Install dependencies
pip install -r requirements.txt
```

### 2. Run the Benchmarking Notebook (2 minutes)

```bash
# Launch Jupyter Lab
jupyter lab hhl_algorithm_benchmarking.ipynb

# In Jupyter: Run > Run All Cells
```

### 3. View Results (1 minute)

The notebook generates:
- `hhl_benchmark_results.csv` - Detailed data
- `hhl_benchmark_results.png` - Visualizations
- `hhl_scalability.png` - Scaling analysis

---

## 📊 What You Get

### Comprehensive Benchmarking
- **Qiskit HHL**: IBM's quantum computing framework
- **PennyLane HHL**: Hybrid quantum-classical ML
- **Classical Baseline**: NumPy solver for comparison

### Performance Metrics
- ⏱️ Runtime comparison
- 🎯 Accuracy (error & fidelity)
- 💻 Resource requirements
- 📈 Scalability analysis

### ML Applications
- Ridge regression
- Linear systems solving
- Support Vector Machines
- Portfolio optimization

---

## 🎯 Which Framework Should You Use?

### Quick Decision Guide

| Your Goal | Recommended Framework |
|-----------|----------------------|
| Production deployment | **Qiskit** |
| Research & prototyping | **PennyLane** |
| Hybrid quantum-classical ML | **PennyLane** |
| IBM Quantum hardware | **Qiskit** |
| Quick experiments | **PennyLane** |
| Large community support | **Qiskit** |

---

## 🔬 Which Tomography Method?

| Scenario | Method | Reason |
|----------|--------|--------|
| Quick validation | **Direct Fidelity** | Fastest |
| Full state needed | **Compressed Sensing** | Efficient |
| Many observables | **Shadow Tomography** | Few measurements |
| Gate characterization | **Randomized Benchmarking** | No tomography |

---

## 📁 Repository Structure

```
dieser-max-tum.github.io/
├── hhl_algorithm_benchmarking.ipynb    # Main benchmarking notebook
├── hhl_advanced_usage.ipynb            # Advanced usage examples
├── requirements.txt                     # Python dependencies
├── HHL_BENCHMARKING_README.md          # Detailed documentation
├── QUICK_START_GUIDE.md                # This file
└── README.md                            # Repository overview
```

---

## 💡 Key Insights from Benchmarking

### When to Use HHL Algorithm

✅ **USE HHL when:**
- Matrix size N > 1000
- Matrix is sparse
- Only need quantum state |x⟩
- Well-conditioned (κ < 100)
- Have quantum hardware access

❌ **DON'T USE HHL when:**
- Small matrices (N < 100)
- Need exact classical solution
- Ill-conditioned matrix
- No quantum hardware available
- Near-term practical application

### Expected Performance

For a **4×4 matrix**:
- Classical: ~0.0001s
- Qiskit HHL: ~0.1-1s (simulator)
- PennyLane HHL: ~0.1-1s (simulator)

**Note**: Quantum advantage appears at larger scales (N > 1000) with appropriate structure

---

## 🔧 Troubleshooting

### Issue: Import errors
```bash
# Solution: Install/upgrade packages
pip install --upgrade qiskit qiskit-aer pennylane
```

### Issue: Memory errors
```python
# Solution: Reduce problem size
problem_sizes = [2, 4]  # Instead of [2, 4, 8, 16]
```

### Issue: Slow execution
```python
# Solution: Reduce trials
n_trials = 1
```

### Issue: Matrix is ill-conditioned
```python
# Solution: Apply preconditioning
condition_num = np.linalg.cond(A)
if condition_num > 100:
    D = np.diag(1 / np.sqrt(np.diag(A)))
    A = D @ A @ D
```

---

## 📚 Next Steps

### Beginner Track (Weeks 1-2)
1. ✅ Run basic benchmarking notebook
2. ✅ Understand the results
3. ✅ Compare different frameworks
4. ✅ Try different problem sizes

### Intermediate Track (Weeks 3-4)
1. Modify matrix conditioning
2. Implement custom solvers
3. Test on different ML problems
4. Optimize tomography methods

### Advanced Track (Weeks 5+)
1. Deploy on real quantum hardware
2. Implement error mitigation
3. Scale to larger problems
4. Publish your results

---

## 🔗 Essential Links

### Documentation
- [Main README](README.md)
- [Detailed Documentation](HHL_BENCHMARKING_README.md)
- [Advanced Usage](hhl_advanced_usage.ipynb)

### Frameworks
- **Qiskit**: https://qiskit.org
- **PennyLane**: https://pennylane.ai
- **Cirq**: https://quantumai.google/cirq

### Learning Resources
- **Qiskit Textbook**: https://qiskit.org/textbook
- **PennyLane Demos**: https://pennylane.ai/qml
- **Quantum Algorithm Zoo**: https://quantumalgorithmzoo.org

### GitHub Repositories
- **Qiskit ML**: https://github.com/Qiskit/qiskit-machine-learning
- **PennyLane**: https://github.com/PennyLaneAI/pennylane
- **QuTiP**: https://github.com/qutip/qutip

---

## 🤝 Contributing

Found a bug? Have an improvement? 

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

---

## 📧 Support

- Open an issue on GitHub
- Check the documentation
- Ask on Qiskit Slack or PennyLane Forum

---

## ⚡ Pro Tips

1. **Start Small**: Begin with 2×2 matrices
2. **Validate Early**: Compare with classical solutions
3. **Monitor Conditioning**: Keep κ < 100
4. **Use Fast Tomography**: DFE for quick checks
5. **Iterate**: Test different frameworks
6. **Document**: Save your configurations
7. **Scale Gradually**: Increase size slowly
8. **Ask for Help**: Use community resources

---

## 📊 Example Results

After running the notebook, you should see:

```
Problem Size: 2x2
  Classical Runtime: 0.000050s
  Qiskit HHL Runtime: 0.250000s
  Error: 0.001234
  Fidelity: 0.9988

Problem Size: 4x4
  Classical Runtime: 0.000080s
  Qiskit HHL Runtime: 0.580000s
  Error: 0.002456
  Fidelity: 0.9975
```

**Interpretation**: Classical is faster for small problems, but quantum methods scale better

---

## 🎓 Learning Path

```
Week 1: Basics
  → Install frameworks
  → Run benchmarking notebook
  → Understand output

Week 2: Exploration
  → Try different problem sizes
  → Compare frameworks
  → Test ML applications

Week 3: Optimization
  → Matrix preconditioning
  → Fast tomography
  → Error analysis

Week 4: Advanced
  → Custom implementations
  → Hardware deployment
  → Production readiness
```

---

## ✅ Checklist Before Starting

- [ ] Python 3.8+ installed
- [ ] pip or conda available
- [ ] Jupyter Lab/Notebook installed
- [ ] 2GB+ RAM available
- [ ] Internet connection (for package download)
- [ ] Text editor (optional)
- [ ] Git (optional)

---

**Ready to start?** 

Run: `jupyter lab hhl_algorithm_benchmarking.ipynb` and explore quantum computing! 🚀

---

*Last updated: 2025*
