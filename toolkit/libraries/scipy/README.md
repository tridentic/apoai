
# SciPy

## Use when
- You need optimization, statistics, linear algebra, signal processing, or special routines missing in NumPy.

## Must-know
- `scipy.optimize.curve_fit`
- `scipy.optimize.linear_sum_assignment`
- `scipy.stats` distributions and tests
- `scipy.linalg`
- `scipy.signal`
- `scipy.sparse`
- `scipy.interpolate`

## Contest heuristics
- Use `curve_fit` for parametric fitting when the model form is known.
- Use `linear_sum_assignment` for assignment/matching problems.
- Use `stats` for sampling, distributions, and lightweight statistical checks.
- Prefer `scipy.linalg` when you need more advanced linear algebra than NumPy provides.
- Use interpolation when the task is reconstruction rather than prediction.
- Use sparse matrices when the data is high-dimensional and mostly zero.

## Gotchas
- `curve_fit` needs a sensible initial guess when the fit is nonlinear.
- `linear_sum_assignment` solves rectangular as well as square assignments.
- Bounds change the fitting method in `curve_fit`.
- Statistical fitting is not the same as neural training; do not overcomplicate a curve-fitting task.

## Sources
- SciPy optimize docs
- `curve_fit`
- `linear_sum_assignment`
- linalg reference