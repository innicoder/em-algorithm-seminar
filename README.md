# The EM Algorithm for Gaussian Mixtures

A seminar paper with its code, written for the PhD course **Machine Learning (20.IDI12)**, Doctoral Academic Studies in Computer Science, Faculty of Sciences and Mathematics, University of Niš.
Mentor: Prof. Branimir Todorović · Author: Elvir Muslić

The paper and the notebook are one version: the notebook computes every number, table and figure of the paper and cites the paper's sections, equations and algorithm by their numbers.

## Contents

| File | What it is |
|---|---|
| [`seminar.pdf`](seminar.pdf) | the paper; `seminar.tex` and `seminar.bib` are its LaTeX source |
| [`project/em_project.ipynb`](project/em_project.ipynb) | the notebook, with its outputs |
| `project/figures/`, `project/data/faithful.csv` | the two figures of the paper, and the Old Faithful data |
| `project/requirements.txt` | the pinned package versions |

## What the notebook does

- **One iteration by hand:** the E-step and the M-step on four points, with NumPy and SciPy, as in Table 1 of the paper.
- **The same iteration with scikit-learn:** `GaussianMixture`, the method of the paper, reproduces it to machine precision.
- **Old Faithful:** EM with `GaussianMixture`, one iteration per call, recording the log-likelihood after every iteration (Algorithm 1).
- **Twenty random starts:** EM can stop at a local maximum, so the fit is repeated from random starting points.

## Results

- **By hand:** one iteration raises the log-likelihood from −11.3689 to −6.3155; scikit-learn agrees to 6.2e-15.
- **Old Faithful** (272 eruptions, two components, a poor start): EM converges in 53 iterations, and the log-likelihood (of the standardized data) rises at every iteration to −385.4607.
- **The fit:** short eruptions (2.04 min, next wait 54.48 min, weight 0.356) and long ones (4.29 min, wait 79.97 min, weight 0.644).
- **Random starts:** all twenty reach the same log-likelihood, in 11 to 37 iterations.

## Run

```bash
cd project
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/jupyter nbconvert --to notebook --execute --inplace em_project.ipynb
```

- The run takes a few seconds and rewrites `project/figures/`.
- Alternatively, open `project/` in VS Code, select the `.venv` kernel and choose Run All.
- To rebuild the paper: `latexmk -pdf seminar.tex` (with biber).

## Credits

- **Theory:** A. P. Dempster, N. M. Laird and D. B. Rubin (1977); C. F. J. Wu (1983); C. M. Bishop, *Pattern Recognition and Machine Learning*, Springer, 2006.
- **Data:** Old Faithful eruptions, R `datasets::faithful`, from the [Rdatasets](https://vincentarelbundock.github.io/Rdatasets/) collection.
- **Software:** scikit-learn, NumPy, SciPy and Matplotlib.
