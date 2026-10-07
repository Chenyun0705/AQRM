#Bosonic-cutoff convergence of the effective Hermitian Hamiltonian
This folder reports the convergence of the lowest 20 eigenenergies of the effective Hermitian Hamiltonian \(H_H\) with respect to the bosonic cutoff \(N\).
Parameters
- \(\Delta=5.0\), \(\epsilon=1.7340\), \(g=4.5\)
- \(\beta=1.0\), \(\zeta_0=1.0\), \(\Omega_0=1.0\)
- \(\bar\Omega=1.000562895442\), \(\bar\zeta=0.998797933904\)
- \(\omega_{\mathrm{eff}}=0.867021787237\)
- Cutoffs: \(N=60,80,100,120,140,160\)
The Hamiltonian was diagonalized with scipy.linalg.eigh. The test was performed at the largest coupling considered, \(g=4.5\), where bosonic truncation effects are expected to be most pronounced.
Main result
For the lowest ten levels, the maximum difference between \(N=100\) and \(N=120\) is
\[
\max_{0\le n\le9}|E_n^{(120)}-E_n^{(100)}|=1.176\times10^{-12}.
\]
For all lowest 20 levels, the corresponding maximum difference is
\[
\max_{0\le n\le19}|E_n^{(120)}-E_n^{(100)}|=4.961\times10^{-7}.
\]
Therefore, \(N=100\) is fully sufficient for the lowest ten levels and provides better than \(10^{-6}\) absolute convergence for the lowest 20 levels under these parameters. For resolving very small splittings involving the highest levels in this table, \(N=120\) may be used as a stricter reference.
Files
- HH_levels_vs_N.csv: lowest 20 energies for every cutoff.
- HH_N100_convergence_check.csv: absolute differences between \(N=100\) and the larger cutoffs \(N=120,140\).
This test establishes convergence of the effective Hermitian Hamiltonian spectrum only. Convergence of selected full Liouvillian modes is checked separately.
