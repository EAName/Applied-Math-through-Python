# Applied-Math-through-Python

Graduate coursework applying linear algebra, discrete mathematics, probability, calculus, and optimization through Python notebooks for data science and engineering foundations.

---

## 1. Title and Summary

**Applied Math through Python**  
Northwestern University M.S. in Data Science (Data Engineering specialization): computational exploration of mathematical models across algebra, probability, graph theory, single- and multivariable calculus, and linear programming using NumPy, SciPy, SymPy, PuLP, and matplotlib.

---

## 2. Concepts and Methods

- **Python numerics foundations:** integer vs. float division, modulo, assignment and expression evaluation (`Basic Calculations.ipynb`)
- **Linear functions and modeling:** slope-intercept lines, break-even analysis, plotting with `linspace` (`Slopes and Lines.ipynb`); correlation coefficient and least-squares line via `scipy.stats.linregress`
- **Linear systems and inequalities:** graph feasible regions for LP constraints; evaluate objective at corner points with NumPy matrices (`Graphing Linear Systems.ipynb`, `Graphing Linear Inequalities.ipynb`, `Solving LP Models Graphically.ipynb`, `More on LP Models.ipynb`)
- **Linear programming solvers:** `scipy.optimize.linprog` (simplex method) and PuLP formulation/solve for max/min problems (`Solving LP Models Using Pulp or SciPy.ipynb`)
- **Matrix algebra:** NumPy arrays, matrix operations, determinants, inverses, solving Ax=b with `numpy.linalg.inv` and `linalg.solve` (`Matrix Operations.ipynb`, `Matrix Inverses.ipynb`)
- **Set theory and probability:** universe generation, set operations, union/intersection probabilities, conditional probability on finite sample spaces (`Sets and Probability.ipynb`)
- **Counting:** recursive factorial, permutations, combinations (`Counting Principles.ipynb`)
- **Continuous probability:** random sampling, histogram binning, empirical distribution exploration (`Continuous Probability.ipynb`); normal CDF via Simpson's rule integration and shaded area plots (`Normal Distribution.ipynb`)
- **Discrete math / graph theory:** custom `Node` and `Graph` classes; adjacency dictionaries; shortest-path search; tree detection (`Graph Theory.ipynb`)
- **Limits and continuity:** numerical limit approximation by shrinking delta; limits at infinity (`Limits.ipynb`)
- **Differentiation:** secant-to-tangent limiting slopes, derivative interpretation, higher-order derivatives (`Rates of Change.ipynb`, `Higher Order Derivatives.ipynb`); relative/absolute extrema with NumPy arrays and matplotlib (`Relative and Absolute Extrema.ipynb`)
- **Integration:** numerical integration routines; Fundamental Theorem applications; area under curves (`Fundamental Theorem of Calculus.ipynb`, `Area and the Definite Integral.ipynb`)
- **Multivariable calculus:** partial derivatives, critical points via SymPy `linsolve`/`nonlinsolve`, Lagrange multipliers for constrained optimization (`Multivariable Calculus Practice.ipynb`)

---

## 3. Stack

| Layer | Tools |
|-------|-------|
| Language | Python 3 |
| Environment | Jupyter Notebook |
| Numerics | NumPy |
| Symbolic math | SymPy (`symbols`, `diff`, `linsolve`, `nonlinsolve`, Lagrange systems) |
| Optimization | SciPy `optimize.linprog`, PuLP |
| Statistics | SciPy `stats.linregress` |
| Visualization | matplotlib |

---

## 4. Structure

```
Applied-Math-through-Python/
├── Basic Calculations.ipynb
├── Slopes and Lines.ipynb
├── Graphing Linear Systems.ipynb
├── Graphing Linear Inequalities.ipynb
├── Solving LP Models Graphically.ipynb
├── Solving LP Models Using Pulp or SciPy.ipynb
├── More on LP Models.ipynb
├── Matrix Operations.ipynb
├── Matrix Inverses.ipynb
├── Sets and Probability.ipynb
├── Counting Principles.ipynb
├── Continuous Probability.ipynb
├── Normal Distribution.ipynb
├── Graph Theory.ipynb
├── Limits.ipynb
├── Rates of Change.ipynb
├── Higher Order Derivatives.ipynb
├── Relative and Absolute Extrema.ipynb
├── Fundamental Theorem of Calculus.ipynb
├── Area and the Definite Integral.ipynb
├── Multivariable Calculus Practice.ipynb
└── README.md
```

- **Organization:** flat notebook sequence aligned to course modules (algebra → probability → discrete math → calculus → multivariable)
- **Reusable modules:** counting helpers and graph `Node`/`Graph` classes defined inline in notebooks
- **Engineering practice:** numerical limits and integrals as computational substitutes for closed form; corner-point LP evaluation; solver-backed LP verification; OOP graph abstractions for path and tree queries

---

**Course context:** Northwestern University, M.S. in Data Science, Data Engineering specialization  
**Repository:** https://github.com/EAName/Applied-Math-through-Python
