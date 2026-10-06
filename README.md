# The EM Algorithm for Gaussian Mixtures

Seminar project for the PhD course **Machine Learning (20.IDI12)**, Doctoral Academic Studies in Computer Science, Faculty of Sciences and Mathematics, University of Niš.
Instructor: Prof. Branimir Todorović · Author: Elvir Muslić

The notebook fits a two-component Gaussian mixture to the 272 Old Faithful eruptions with the expectation-maximization (EM) algorithm, written in PyTorch in double precision, and reproduces every number, table and figure of the seminar paper. It verifies its results with 13 checks, which stop the run if any checked value deviates.

## Results

- **One iteration by hand** on x = (1, 2, 6, 7): the responsibilities, weights, means and variances match the paper's table to 1e-4; the step raises the log-likelihood from −11.3689 to −6.3155.
- **Old Faithful** (K = 2, 272 eruptions, deliberately poor start): EM converges in 53 iterations to log-likelihood −385.4607. The fit separates short eruptions (2.04 min, next wait 54.5 min, weight 0.356) from long ones (4.29 min, wait 80.0 min, weight 0.644).
- **Checks of the theory:** the log-likelihood never decreases; the weights sum to one and the covariances stay symmetric positive definite after every M-step; the M-step output beats 20 random perturbations in Q; at the fixed point one more EM step changes no parameter (largest change 0) and the gradient with respect to the means is at most 5.6e-13.
- **scikit-learn 1.9.1** from the same start stops after 52 iterations; the two log-likelihoods differ by 2.2e-11.
- **20 random starts** all reach the same limit, −385.4607, in 10 to 31 iterations each.

## Run

```bash
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/jupyter nbconvert --to notebook --execute --inplace em_project.ipynb
```

- Tested with Python 3.14. The reported run took 1.01 s.
- The run rewrites `figures/` and `results.json`.

## Files

| File | Contents |
|---|---|
| `em_project.ipynb` | the notebook, with outputs |
| `results.json` | the key numbers written by the run |
| `figures/` | the two figures, `em_iterations.pdf` and `em_loglik.pdf` |
| `data/faithful.csv` | Old Faithful eruptions, R `datasets::faithful`, from the [Rdatasets](https://vincentarelbundock.github.io/Rdatasets/) collection |
| `requirements.txt` | pinned package versions |
