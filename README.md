# The EM Algorithm: Implementation and Verification

Seminar project for the PhD course **Machine Learning (20.IDI12)**, Doctoral Academic Studies in Computer Science, Faculty of Sciences and Mathematics, University of Niš.
Instructor: Prof. Branimir Todorović · Author: Elvir Muslić

The notebook implements the expectation–maximization (EM) algorithm in PyTorch (double precision). It checks its results with 35 assertions, which stop the run if any checked value deviates.

## Results

- **Genetic linkage** (Dempster, Laird & Rubin, 1977):
  - Starting from θ = 0.5, EM converges to θ̂ = (15 + √53809)/394 = 0.6268214979.
  - The ratio of successive errors settles at 0.13278. This equals the fraction of missing information, I_m / I_c = 57.80 / 435.32.
- **Gaussian mixture on Old Faithful** (K = 2, 272 eruptions):
  - Converges in 53 iterations to log-likelihood −385.4607.
  - scikit-learn 1.9.1 reaches the same fit (difference 0.0) in 52 iterations.
- **Monotone ascent and multiple limits:**
  - Across 60 runs (6410 EM iterations), the log-likelihood never decreases beyond rounding.
  - With K = 3, different starts reach different limits; the best is −369.6366.

## Run

```bash
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/jupyter nbconvert --to notebook --execute --inplace em_project.ipynb
```

- Tested with Python 3.14. The reported run took 9.23 s.
- The run rewrites `figures/` and `results.json`.

## Files

| File | Contents |
|---|---|
| `em_project.ipynb` | the notebook, with outputs |
| `results.json` | the key numbers written by the run |
| `figures/` | the four figures |
| `data/faithful.csv` | Old Faithful eruptions, R `datasets::faithful`, from the [Rdatasets](https://vincentarelbundock.github.io/Rdatasets/) collection |
| `requirements.txt` | pinned package versions |
