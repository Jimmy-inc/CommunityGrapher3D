# CommunityGrapher3D

A Desmos-style 3D graphing calculator, built for topology and multivariable calculus. Type math the way you write it, and the app works out what you mean: Cartesian, cylindrical or spherical coordinates, a surface, a solid, a curve, a set, a sequence or a plain calculation.

**→ Read the full [User Guide](docs/USER_GUIDE.md).**

## Features

- **Detects your coordinate system.** `z = sin(x)cos(y)` is drawn in Cartesian coordinates, `r = 2 + cos(4θ)` in cylindrical and `ρ = 1 − cos φ` in spherical. Spell names however you like: `rho`, `roh`, `ρ`, `\theta`.
- **Desmos-style typing.** `^` raises the cursor, `/` makes a fraction, and `theta` turns into θ.
- **Surfaces, curves and points:** explicit, implicit and parametric (`t` for a curve, `u, v` for a surface).
- **Inequalities as solids,** drawn see-through with solid border lines, e.g. `ρ ≤ 2, φ ≤ π/6`.
- **Set-builder notation** in 3D and in the plane: `{(x, y, z) : x² + y² + z² = 1, z ≥ 0}`, `{(r, θ) : r ≤ 1 + cos θ}`. Convert a set between coordinate systems with one click.
- **Matrices.** Type `A = Matrix` to get an editable matrix you can resize by dragging its corner. Apply it to vectors and to whole sets: `A{…}`, with a **Show both** before/after view.
- **Functions on sets.** Define `f(a, b, c) = (3a, 2b, 4c)`, then draw `f({(a, b, c) : …})` or `f(A)`. Input and output dimensions (ℝⁿ → ℝᵐ) are detected and checked.
- **Sequences:** `seq(k)(1/k, 1/(3k), 1/(2k))`, drawn as dots joined in order, from 1 up to ∞.
- **Sliders:** any unknown letter becomes a slider, and you can animate it.
- **Calculator:** `1+1` shows `= 2`, with a fraction toggle.
- **Fly mode:** walk through your graph as a 3D world, with WASD and mouse-look, and a render distance of up to 1000.
- **Display settings:** scale up to ±1000, a resolution slider, Math/Physics angle conventions, an FPS counter, a collapsible sidebar and dark mode.

## Quick start

1. Download [`CommunityGrapher3D.html`](CommunityGrapher3D.html).
2. Double-click it to open it in a modern browser, such as Chrome, Edge, Firefox or Safari.
3. Start typing in the sidebar.

It's a single file with nothing to install. You need an internet connection the first time it loads, because it gets three.js, math.js and MathQuill from public CDNs.

## Built with

[three.js](https://threejs.org/) for 3D rendering, [math.js](https://mathjs.org/) for parsing, and [MathQuill](http://mathquill.com/) for the math input.
