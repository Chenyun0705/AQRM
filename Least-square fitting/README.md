# Least-square fitting for the Brownian-oscillator correlation function

This folder contains the least-square fitting code used to obtain the effective parameters reported in the manuscript.

## File structure

```text
Least-square fitting/
├── Least-square Fitting.ipynb
├── README.md
└── deom/
    ├── __init__.py
    ├── deom.py
    └── spectrum/
        ├── __init__.py
        ├── aaa.py
        ├── aux.py
        ├── esprit.py
        ├── pade.py
        └── prony.py
```

The `deom` folder must be placed in the same parent folder as `Least-square Fitting.ipynb`.

The bundled `deom` source files are necessary for the least-square fitting:

- `deom/__init__.py` initializes the `deom` package and makes `decompose_spe` available to the notebook.
- `deom/deom.py` contains the implementation of `decompose_spe`, which is used to decompose the Brownian-oscillator spectrum and construct the original correlation function.
- `deom/spectrum/` contains the spectral-decomposition modules imported by `deom.py`. These source files must remain in the displayed directory structure.

Generated cache folders such as `__pycache__/` and compiled files such as `*.pyc` are not required and are not included.

Do not rename the `deom` folder to `DEOM`, because the notebook imports it with:

```python
from deom import decompose_spe
```

Folder names are case-sensitive on Linux.

## Least-square fitting definition

The Brownian-oscillator response function is

$$
\chi(\omega)=\frac{\Omega_0}{\Omega_0^2-\omega^2-i\zeta_0\omega}.
$$

The parameters used for the first parameter set in Table I are

```text
beta   = 1.0
Omega0 = 1.0
zeta0  = 1.0
Delta  = 5.0
npsd   = 1500
```

The correlation function is fitted by

$$
C_{\mathrm{fit}}(t)=\eta_+e^{-\gamma_+t}+\eta_-e^{-\gamma_-t}.
$$

The fitting interval is $0\le t\le80$, with 10,001 uniformly spaced time points. Uniform weighting is used, and the residual vector is

$$
\mathbf r=
[\operatorname{Re}(C_{\mathrm{fit}}-C),
\operatorname{Im}(C_{\mathrm{fit}}-C)].
$$

The five real fitting parameters are introduced through

$$
\gamma_\pm=a\pm i\sqrt b,\qquad
\eta_+=c+id,\qquad
\eta_-=e-id.
$$

The initial guess for $[a,b,c,d,e]$ is `[0.5, 1.0, 1.0, 0.0, 1.0]`.

## Output

Running the notebook prints:

- the least-square fitting interval, weighting, residual definition, and optimizer status;
- the fitted values of $\eta_\pm$ and $\gamma_\pm$ and their formal fitting errors;
- the derived effective parameters;
- the SSE, RMSE, maximum absolute error, and relative $L_2$ error.

The notebook also displays the time-domain and frequency-domain comparison figures. It does not save data or figures to disk.

The reported formal $1\sigma$ errors are calculated from the local least-square fitting covariance matrix under the uniform independent-residual assumption. They are fitting-error estimates, not experimental confidence intervals.

## Requirements and execution

The calculation was performed using Python 3.7.0, NumPy 1.15.1, and SciPy 1.1.0. SymPy, Matplotlib, and Pandas are also required.

Open `Least-square Fitting.ipynb`, select the intended Python environment, and run all cells from the beginning. No package upgrade is required if all imports work in the existing environment.
