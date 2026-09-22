# Hyperbolic Taxicab Geometry

> Summer research building a new metric space from the ground up: the upper half-plane, but with a taxicab twist on the hyperbolic metric. We work out what its straight lines look like, prove exactly which maps preserve distance, and ask whether the space is "negatively curved" in the coarse sense.

---

## The Problem

Two of the most studied objects in geometry are the **hyperbolic plane** (the model of negatively curved space) and **taxicab geometry** (where distance is measured in city blocks, `|Δx| + |Δy|`, not straight-line). Each is well understood on its own. This project asks what happens when you **merge them**.

We take the upper half-plane and put a *hyperbolic taxicab norm* on it: the usual taxicab norm, but reweighted by height so that distances stretch near the boundary the way they do in hyperbolic space. The result is a brand-new metric space, and almost nothing about it is obvious. What is the distance between two points? What do the "straight lines" (geodesics) look like? Which transformations are symmetries? Is the space Gromov hyperbolic, the coarse notion of negative curvature that matters in modern geometry?

Answering those questions was the summer's work.

---

## The Setup

The space is the upper half-plane

```
H_T = { (x1, x2) in R^2 : x2 > 0 }
```

with the **hyperbolic taxicab norm** at a point `p`:

```
||v||_p = (1 / p2) * ||v||_T
```

where `||v||_T = |v1| + |v2|` is the ordinary taxicab (L1) norm and `p2` is the height. Dividing by the height is what makes it hyperbolic: the same physical step counts as more distance the closer you are to the boundary line `x2 = 0`.

Integrating that norm along curves gives a genuine distance function, and that is where the geometry starts to get interesting.

---

## What We Proved

### 1. The distance function
We derived a closed form for the distance between any two points:

```
d(p, q) = ln(μ / p2) + ln(μ / q2) - (1/μ) * |q1 - p1|,   where μ = max{ p2, q2, ½|q1 - p1| }
```

The `μ` term is doing real work: which of the three quantities is largest decides which *kind* of shortest path connects the two points.

### 2. The geodesics (shortest paths)
We classified every length-minimizing curve in the space. They come in a small, tidy list:
- **vertical segments**
- **horizontal segments of length 2 or less**
- **L-shaped "λ" curves** (go across, then up/down)
- **"η" curves** (up to a peak, across, then back down)

A memorable fact fell out of the algebra: the horizontal part of an η geodesic always has length **exactly 2**, no matter which two points it connects.

### 3. The isometries (distance-preserving maps)
We proved that the symmetries of this space are exactly:
- **horizontal translations**
- **reflections across vertical lines**
- **dilations centered on the boundary line at infinity**
- and compositions of these.

The hard direction is showing there are *no others*. The proof leans on the fact that any isometry has to send geodesics to geodesics, so it must map vertical segments to vertical segments and horizontal to horizontal, which pins down its form. We also showed the tempting candidate `(x1, x2) -> (x1, 1/x2)` is *not* an isometry, because it distorts the length of horizontal segments.

### 4. Gromov hyperbolicity and beyond
We investigated whether the space is **Gromov hyperbolic** (the coarse, large-scale version of negative curvature), and began extending the whole construction to **generalized boundaries**, replacing the horizontal line at infinity with a line of arbitrary slope `m` and finding the reweighted norm that keeps the geometry consistent.

---

## What the Code Does

The Mathematica notebook is the visual companion to the proofs. It:
- plots points and the **geodesics** between them (the vertical, L-shaped λ, and η curves), so we could see the shortest-path classification before proving it
- evaluates and visualizes the **distance function** across the half-plane
- let us test conjectures quickly by drawing pictures, for example checking that η's horizontal component really is always length 2

The pictures in the conference talk were generated from this notebook.

---

## Tech Stack

| Tool | Used for |
|------|----------|
| Wolfram Mathematica | Symbolic geometry, geodesic plots, distance-function visualizations |

---

## Results / Output

- A full research writeup: *Taxicab Geometry Notes, Summer 2025*
- A conference talk: *Geodesics and Hyperbolicity for Half-Plane Models of Taxicab Hyperbolic Space*, presented at the **PNW-MAA meeting, April 2026**

---

## Try It Yourself

```
git clone https://github.com/klin61027/hyperbolic-taxicab-geometry.git
```

Open `src/` in Wolfram Mathematica (or the free Wolfram Player) and evaluate the notebook top to bottom. The `docs/` folder has the writeup and the talk if you would rather read the math than run it. A PDF export of the notebook is included so you can see the figures without Mathematica.

---

## Honest Notes

- This is **ongoing research**, not a finished paper. Some sections of the notes are still in draft, and the Gromov-hyperbolicity and general-slope results were the open threads at the end of the summer.
- The code is a **research scratchpad** for making figures and testing ideas, not a polished library. It is organized around the pictures in the talk.

---

## Team

Summer 2025 research group: **D. Helliwell, L. Lawrence, Kevin Lin (林敬智), A. Potapyev, A. Siple**, Seattle University.
Conference talk (PNW-MAA, April 2026): **Luka Lawrence, Kevin Lin, Alina Potapyev.**
Advised by **Dr. Helliwell.**

---

## Repository Layout

```
hyperbolic-taxicab-geometry/
├── README.md                          # You are here
├── src/
│   └── taxicab_geometry.nb            # Mathematica notebook (geodesic + distance figures)
├── results/
│   └── figures/                       # exported plots (PNG/PDF)
└── docs/
    ├── taxicab_geometry_notes.pdf     # Summer 2025 research writeup
    └── PNW_MAA_2026_talk.pdf          # Conference presentation
```
