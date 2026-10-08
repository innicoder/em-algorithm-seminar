# The EM Algorithm for Gaussian Mixtures

A seminar (study) project for the PhD course **Machine Learning (20.IDI12)**, Doctoral Academic Studies in Computer Science, Faculty of Sciences and Mathematics, University of Niš. It is course work, not research: it works through standard material for the seminar paper.
Instructor: Prof. Branimir Todorović · Author: Elvir Muslić

The notebook computes one EM iteration by hand with NumPy and SciPy and compares it with one iteration of scikit-learn's `GaussianMixture`. It then fits a two-component Gaussian mixture to the 272 Old Faithful eruptions with `GaussianMixture`, run one iteration at a time so that the log-likelihood can be recorded after every iteration. It produces every number, table and figure of the seminar paper.

## Results

- **One iteration by hand** on x = (1, 2, 6, 7): the step raises the log-likelihood from −11.3689 to −6.3155. One iteration of `GaussianMixture` from the same start gives the same weights, means and variances (largest difference 6.2e-15).
- **Old Faithful** (K = 2, deliberately poor start): EM converges in 53 iterations to log-likelihood −385.4607, and the log-likelihood rises at every iteration (smallest change 2.2e-11). The fit separates short eruptions (2.04 min, next wait 54.5 min, weight 0.356) from long ones (4.29 min, wait 80.0 min, weight 0.644).
- **20 random starts** all reach the same log-likelihood, in 11 to 37 iterations each.

## Run

```bash
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/jupyter nbconvert --to notebook --execute --inplace em_project.ipynb
```

Or open `em_project.ipynb` in VS Code, select the `.venv` kernel and click Run All.

- Tested with Python 3.14.7. The run takes a few seconds.
- The run rewrites `figures/`.

## Files

| File | Contents |
|---|---|
| `em_project.ipynb` | the notebook, with outputs |
| `figures/` | the two figures, `em_iterations.pdf` and `em_loglik.pdf` |
| `data/faithful.csv` | Old Faithful eruptions, R `datasets::faithful`, from the [Rdatasets](https://vincentarelbundock.github.io/Rdatasets/) collection |
| `requirements.txt` | pinned package versions |
