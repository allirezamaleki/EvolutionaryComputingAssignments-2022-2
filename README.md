# Evolutionary Computing Assignments

This repository contains assignments from the Evolutionary Computing course (2022-2). The work demonstrates the application of evolutionary algorithms to solve multi-objective optimization problems, comparing a manual approach with a state-of-the-art evolutionary framework.

---

## Problem: Multi-Objective Cone Optimization

The core problem explored in this project is the **geometric optimization of a cone** under a volume constraint. Two competing objectives must be minimized simultaneously:

| Objective | Formula |
|-----------|---------|
| Lateral surface area (S) | S = π · r · √(r² + h²) |
| Total surface area (T)   | T = π · r · √(r² + h²) + π · r² |

**Constraint:** The cone's volume must exceed 200 cubic units.

> V = (π · r² · h) / 3 > 200

**Search space:**
- Radius: r ∈ [0, 10]
- Height: h ∈ [0, 20]

Because minimizing S and T are conflicting objectives (e.g., a wider base increases T but reduces height requirements), no single optimal solution exists. Instead, the goal is to find the **Pareto frontier** — the set of solutions where no objective can be improved without worsening another.

---

## Approaches

### 1. Manual Multi-Objective Optimization (`Cones_multiObjective(Final Solution).ipynb`)

A from-scratch implementation of Pareto frontier computation:

- **Grid search** over a 10×10 sample of (r, h) pairs within the search space.
- Filters out infeasible solutions that violate the volume constraint.
- Implements **dominated solution filtering** manually to identify the Pareto-optimal set.
- Visualizes feasible solutions against the discovered Pareto frontier.

**Key result:** Identified Pareto-optimal solutions including a point with S ≈ 189.41 and T ≈ 224.32.

---

### 2. Evolutionary Optimization with NSGA-II (`Pymoo.ipynb`)

The same cone problem is re-formulated and solved using the [Pymoo](https://pymoo.org/) evolutionary optimization framework:

- **Algorithm:** NSGA-II (Non-dominated Sorting Genetic Algorithm II)
- **Population size:** 100 individuals
- **Generations:** 100
- **Variables:** 2 (r, h)
- **Objectives:** 2 (S, T)
- **Constraints:** 1 inequality constraint (volume > 200)

NSGA-II is a well-known multi-objective evolutionary algorithm that uses non-dominated sorting and crowding distance to maintain a diverse Pareto-optimal population over successive generations. This approach efficiently searches the solution space through population-based evolution rather than exhaustive enumeration.

---

## Repository Contents

| File | Description |
|------|-------------|
| `Cones_multiObjective(Final Solution).ipynb` | Manual Pareto frontier computation for cone optimization |
| `Pymoo.ipynb` | NSGA-II solution using the Pymoo framework |
| `EC_MultiObjective-report.pdf` | Full written report on the multi-objective optimization problem and results |
| `project-phase.pdf` | Project phase description and requirements |

---

## Requirements

- Python 3.x
- [NumPy](https://numpy.org/)
- [Matplotlib](https://matplotlib.org/)
- [Pymoo](https://pymoo.org/) (`pip install pymoo`)

---

## Concepts Covered

- Multi-objective optimization
- Pareto optimality and Pareto frontier
- Dominated vs. non-dominated solutions
- NSGA-II (Non-dominated Sorting Genetic Algorithm II)
- Constraint handling in evolutionary algorithms
- Comparison of grid search vs. evolutionary search
