# Applied-Math-through-Python

Northwestern University, M.S. in Data Science (Data Engineering specialization) · MSDS 400: Math for Modelers

## Overview

This is the quantitative foundation course of the degree: linear algebra, linear programming, probability, calculus, and graph theory, each worked computationally in Python rather than by hand. The notebooks are short and exercise-sized. The parts that carry forward most directly into data engineering work are the LP formulations (resource allocation as constraints plus an objective), matrix algebra for solving linear systems, and graph traversal over an adjacency structure.

## Highlights / Results

All values below are taken from saved cell outputs in the notebooks.

| Work | Method | Result | Source |
|------|--------|--------|--------|
| Primal LP: maximize 6x1 + 5x2 + 3x3 under three resource constraints | `scipy.optimize.linprog` | Optimal value 9 at x1 = 1.5, x2 = x3 = 0 (printed as -9.0 because the max is posed as a min) | `Solving LP Models Using Pulp or SciPy.ipynb` |
| Dual of the same LP: minimize 12y1 + 6y2 + 8y3 | PuLP | y = (0, 1.5, 0), objective 9, matching the primal (strong duality) | `Solving LP Models Using Pulp or SciPy.ipynb` |
| Minimization LP: 22y1 + 44y2 + 33y3 with three covering constraints | `linprog` and PuLP | Both solvers return y1 = 3, y2 = y3 = 0, objective 66 | `Solving LP Models Using Pulp or SciPy.ipynb` |
| Product-mix revenue model (three products, capacity 210, mix constraints) | PuLP, maximize | (60, 30, 120), maximum revenue $141,000 | `Solving LP Models Using Pulp or SciPy.ipynb` |
| Two-variable LPs solved graphically | Corner-point evaluation with NumPy matrix product | Objective 3x + 4y peaks at 12 at corner (0.8, 2.4); objective 6x + 5y evaluates to 25, 24, 27 at corners (0,5), (4,0), (2,3) | `Solving LP Models Graphically.ipynb`, `More on LP Models.ipynb` |
| 3x3 linear system Ax = b | `numpy.linalg.inv` and `linalg.solve` | Both give x = (13, 1, 20); a singular matrix example shows inverse entries on the order of 1e15 | `Matrix Inverses.ipynb` |
| Weighted graph shortest path, a to c | Recursive path enumeration, minimum total weight | Paths [a,b,c] and [a,d,c]; shortest is [a,d,c] | `Graph Theory.ipynb` |
| Constrained optimization (maximize xy subject to a fixed-area constraint) | SymPy Lagrange multipliers | x = y = 142.48, area 20,300.77 | `Multivariable Calculus Practice.ipynb` |
| Least-squares trend line | `scipy.stats.linregress` | slope -0.506, intercept 87.9, r = -0.941 | `Slopes and Lines.ipynb` |
| Card-draw probability (exactly two aces in five cards) | Hand-written combinations | about 0.0399 | `Counting Principles.ipynb` |

## Engineering decisions and tradeoffs

- **Two solvers on the same LP.** `Solving LP Models Using Pulp or SciPy.ipynb` solves each problem with both `linprog` and PuLP. `linprog` wants every problem as a minimization with `<=` constraints (so maxima are negated and `>=` rows are sign-flipped), while PuLP takes the model as written. Cross-checking caught nothing wrong here, but it is the habit that matters: two independent formulations agreeing is cheap validation.
- **Solving the primal and the dual.** The first LP is solved as a maximization in SciPy and its dual as a minimization in PuLP; both reach 9. This is the clearest piece of rigor in the repo, since it checks the formulation rather than just the arithmetic.
- **Graphical method as a check on solvers.** The two-variable LPs plot the feasible region with matplotlib and then evaluate the objective at each corner with a single matrix product (`corners @ obj`), instead of looping over points.
- **`inv` versus `solve`.** `Matrix Inverses.ipynb` solves the same system both ways, then inverts a singular matrix to show what numerical failure looks like (entries near 1e15 instead of an exception). `linalg.solve` is the right default; explicit inverses are shown for teaching.
- **Graph as classes over an adjacency dict.** `Graph Theory.ipynb` builds `Node` and `Graph` classes from an adjacency matrix and implements path enumeration, path weight, shortest path, and a connectivity check. It is readable, but see the limitations below on algorithmic cost.
- **Numerical over closed form.** Limits are approximated by shrinking a step size, integrals by trapezoid and Simpson's rule, and the normal CDF by integrating the density. This is how the same quantities get computed when no closed form is available.

## Limitations and what I would do differently today

- The `shortest_path` method is commented as Dijkstra but actually enumerates every simple path and picks the lightest. That is exponential in the worst case. Today I would use a priority-queue Dijkstra (or `networkx`), and Bellman-Ford for the negative edge weight that appears in the example graph.
- `is_tree` only checks that the graph is connected, so the 4-cycle "square graph" is reported as a tree. A correct check also needs `edges == nodes - 1` (or cycle detection).
- `linprog` is called with a `method='simplex'` variable that is never passed, so the solver used was SciPy's default, not simplex. The near-zero values like 1.3e-10 in the output are consistent with an interior-point method.
- Some notebooks use `input()` and stale outputs: the binomial cell in `Counting Principles.ipynb` was run with invalid inputs (k > n, p = 2) and prints negative probabilities, and the printed matrix in `Matrix Inverses.ipynb` comes from an earlier version of the cell than the code now shown. `Normal Distribution.ipynb` saved a `TypeError` from passing `alpha` as a string. I left outputs as they were from the original run.
- No tests and no shared module. The counting helpers and graph classes are defined inline. I would move them into a small package with pytest cases (for example, known LP optima and known shortest paths) and run the notebooks headless in CI with `nbmake` or `papermill`.

## Repository map

Ordered by area, with the notebooks most relevant to data engineering first.

**Linear programming and optimization**

| Notebook | Topic |
|----------|-------|
| `Solving LP Models Using Pulp or SciPy.ipynb` | LP formulation and solve with `scipy.optimize.linprog` and PuLP; primal and dual; product-mix revenue model |
| `Solving LP Models Graphically.ipynb` | Feasible region plotting; corner-point evaluation with NumPy matrices |
| `More on LP Models.ipynb` | Feasible region shading between constraint lines; corner-point evaluation |
| `Graphing Linear Inequalities.ipynb` | Plotting constraint half-planes |
| `Graphing Linear Systems.ipynb` | Plotting intersecting lines and feasible regions |
| `Multivariable Calculus Practice.ipynb` | Partial derivatives, critical points via SymPy `linsolve`/`nonlinsolve`, second-derivative test, Lagrange multipliers |
| `Relative and Absolute Extrema.ipynb` | Locating extrema with NumPy arrays and matplotlib |

**Linear algebra**

| Notebook | Topic |
|----------|-------|
| `Matrix Inverses.ipynb` | Matrix inverse, identity check, solving Ax = b with `inv` and `linalg.solve`, singular matrix behavior |
| `Matrix Operations.ipynb` | Lists vs. NumPy arrays, indexing and slicing, elementwise arithmetic, scalar multiplication |
| `Slopes and Lines.ipynb` | Slope-intercept lines, break-even analysis, least-squares line with `scipy.stats.linregress` |

**Graph theory**

| Notebook | Topic |
|----------|-------|
| `Graph Theory.ipynb` | `Node`/`Graph` classes from an adjacency matrix; all paths, weighted shortest path, connectivity (`is_tree`) |

**Probability and counting**

| Notebook | Topic |
|----------|-------|
| `Sets and Probability.ipynb` | Set operations, union rule, odds, conditional probability, product rule on a finite sample space |
| `Counting Principles.ipynb` | Recursive factorial, permutations, combinations, binomial distribution, card-draw probability |
| `Continuous Probability.ipynb` | Random sampling and histogram binning |
| `Normal Distribution.ipynb` | Standard normal density; CDF by Simpson's rule; shaded area plot |

**Calculus**

| Notebook | Topic |
|----------|-------|
| `Limits.ipynb` | Numerical limits by shrinking delta; limits at infinity |
| `Rates of Change.ipynb` | Secant-to-tangent slopes; tangent line plots |
| `Higher Order Derivatives.ipynb` | `numpy.poly1d` derivatives, integrals, and roots |
| `Area and the Definite Integral.ipynb` | Riemann-style area estimates |
| `Fundamental Theorem of Calculus.ipynb` | Trapezoid-rule integration; shaded area plots |

**Python basics**

| Notebook | Topic |
|----------|-------|
| `Basic Calculations.ipynb` | Integer vs. float division, modulo, expression evaluation |

## Reproducing

- The notebooks were last run on Python 3.8 (per notebook metadata) with NumPy 1.x.
- Install dependencies: `pip install -r requirements.txt`, then `jupyter notebook`.
- No external datasets are used; all inputs are defined in the notebooks.
- `Normal Distribution.ipynb` imports `numpy.math` and `Matrix Inverses.ipynb` imports `numpy.linalg.linalg`. Both were removed in NumPy 2.0, so use `pip install "numpy<2"` if you want those two to run unchanged.
- A few cells call `input()` and wait for a value.
- Saved outputs reflect the original course run and were not regenerated.

## Stack

| Layer | Tools |
|-------|-------|
| Language | Python 3 |
| Environment | Jupyter Notebook |
| Numerics | NumPy |
| Symbolic math | SymPy (`symbols`, `diff`, `linsolve`, `nonlinsolve`, Lagrange systems) |
| Optimization | SciPy `optimize.linprog`, PuLP |
| Statistics | SciPy `stats.linregress` |
| Visualization | matplotlib |
