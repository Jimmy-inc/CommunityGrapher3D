# CommunityGrapher3D — User Guide

CommunityGrapher3D is a 3D graphing calculator that reads math the way you write it. This guide covers everything it can do, from the first line you type to functions on sets and flying through your graph.

## Contents

1. [Getting started](#1-getting-started)
2. [A tour of the screen](#2-a-tour-of-the-screen)
3. [Typing math](#3-typing-math)
4. [Coordinate systems and auto-detection](#4-coordinate-systems-and-auto-detection)
5. [Surfaces](#5-surfaces)
6. [Solids from inequalities](#6-solids-from-inequalities)
7. [Curves, parametric surfaces and points](#7-curves-parametric-surfaces-and-points)
8. [Sliders and constants](#8-sliders-and-constants)
9. [The calculator](#9-the-calculator)
10. [Sets (set-builder notation)](#10-sets-set-builder-notation)
11. [Matrices](#11-matrices)
12. [Functions](#12-functions)
13. [Sequences](#13-sequences)
14. [Moving around: Orbit mode](#14-moving-around-orbit-mode)
15. [Fly mode](#15-fly-mode)
16. [Settings reference](#16-settings-reference)
17. [Reference: functions, constants and operators](#17-reference-functions-constants-and-operators)
18. [Messages and troubleshooting](#18-messages-and-troubleshooting)

---

## 1. Getting started

1. Download `CommunityGrapher3D.html` from this repository.
2. Double-click it. It opens in your default browser.
3. The app starts with a few example graphs. Click any line in the sidebar and start typing.

**Requirements**

- A modern browser with WebGL, such as Chrome, Edge, Firefox or Safari.
- An internet connection when the page loads. The app gets three.js, math.js, MathQuill and its fonts from public CDNs.
- Nothing to install, and no account. Everything runs in your browser.

---

## 2. A tour of the screen

### The sidebar (left)

| Part | What it does |
|---|---|
| **CommunityGrapher3D** title and **«** | **«** hides the sidebar so the graph fills the window. Bring it back with **» Expressions** at the top left of the graph. The app remembers your choice in this browser. |
| **Keypad** | Buttons that insert symbols into the line you're editing: ρ θ φ π, √, a⁄b (fraction), ≤ ≥, xⁿ (exponent), x² (squared), ( ), { } (set braces), ∈, ∪ (union) and ∩ (intersection). |
| **Expression list** | One math line per row. Each row has a coloured dot, the line itself and a **×** to delete it. Under the line you may see a coloured *chip* that says what the line was read as, a *reads as* note, sliders, range boxes and buttons. |
| **Click empty space to add an expression** | Click anywhere in the empty area below your lines to add a new line. If the last line is already empty, it's reused. |
| **Add an example…** | A menu of ready-made graphs to add. |
| **README** | A short in-app cheat sheet. |
| **Settings** | Orbit/Fly, Math/Physics, Scale (or Render distance in fly mode), Scroll to zoom, and Resolution. See [Settings reference](#16-settings-reference). |

### The graph (right)

| Part | What it does |
|---|---|
| **FPS counter** (top right) | Frames per second, in green (50+), yellow (25–49) or red (below 25). Click it to dim it. |
| **Legend** (bottom left) | In orbit mode, a reminder of what θ and φ mean. In fly mode, the controls, your speed and how much of the world has been built. |
| **Reset view** (bottom right) | Puts the camera back to the starting view. |
| **Fly pad** (fly mode only) | On-screen **Rise**, **Sink**, **▲** and **▼** buttons for touch screens. |

### Each line's controls

- **Coloured dot:** click it to show or hide that graph. A hidden graph's dot is hollow. A function that other lines use starts hidden.
- **Chip:** what the app understood, e.g. **SPHERICAL ρ = f(θ, φ)**, **CYLINDRICAL implicit surface**, **Planar set**, **Function ℝ³ → ℝ³**, **Sequence in k**.
- **Coordinate menu** (*Auto-detect / Cartesian / Cylindrical / Spherical*): appears on surfaces and solids. Use it to override the detected system.
- **reads as …:** appears when the app reinterpreted something you typed, such as splitting `xy` into x·y or reading `roh` as ρ, so you can check it understood correctly.
- **Red message:** an explanation of what's wrong, or what's missing.

On small screens such as phones, the graph sits on top and the list below it.

---

## 3. Typing math

The input works like Desmos: what you type is shown as real math.

| You type | You get |
|---|---|
| `^` | The cursor moves up into an exponent. Press **→**, or type `+ - = < > , )`, to come back down. |
| `/` | A fraction, with what you typed before it on top. Keep typing to fill the bottom. |
| `sqrt` | A square root sign. |
| `theta`, `phi`, `rho`, `pi`, `tau` | θ, φ, ρ, π, τ. Also `alpha`, `beta`, `gamma`, `delta`, `epsilon`, `lambda`, `mu`, `sigma`, `omega`. |
| `sin`, `cos`, `ln`, `abs`, … | Shown upright as function names. |
| `(` or `{` | A matching pair of brackets. |
| `<=`, `>=` | ≤ and ≥ (or use the keypad). |

**Keyboard**

- **Enter** adds a new line below the current one.
- **Backspace** on an empty line deletes it and moves to the line above.
- **← →** move through the math, entering and leaving exponents and fractions.

**Writing things naturally**

- Multiplication can be implied: `2x`, `xy`, `rsinφ`, `a(x+1)`.
- Run-together letters are split into known names: `xy` is read as x·y, `rz` as r·z, `rsinθ` as r·sin θ. The *reads as* note shows how it was split.
- A letter with a subscript is one name: `a_1` (type `a_1`) is a single variable, and `a_1x` and `xa_1` are both x·a₁.
- Functions can be stacked without brackets: `sin cos x` is sin(cos x).
- `sin^2(x)` means (sin x)².
- `|x|` is the absolute value.
- `n!` is the factorial. It works for non-whole numbers too, through the gamma function.
- `a mod b` is the remainder.

---

## 4. Coordinate systems and auto-detection

You don't pick a coordinate system. The app reads the variables you use.

| Variables used | System | Example |
|---|---|---|
| `x y z` | Cartesian | `z = sin(x)cos(y)` |
| `r θ z` | Cylindrical | `r = 2 + cos(4θ)` |
| `ρ θ φ` | Spherical | `ρ = 1 − cos(φ)` |
| Cartesian and polar together, like `x` with `ρ` | Mixed: solved as an implicit surface in x, y, z | `ρ = 2 + sin(3x)/3` |

**How it decides** (Math convention):

- Only x, y, z → Cartesian.
- If φ (the angle down from +z) appears → spherical.
- Otherwise, if z appears with r or θ → cylindrical.
- ρ on its own (without r) → spherical; r on its own → cylindrical.

When it has to choose, a note explains it, e.g. "ρ read as spherical radius".

**Spellings it understands:** `rho`, `roh`, `rhoo`, `ρ`, `\rho`, `theta`, `teta`, `thetha`, `θ`, `phi`, `phy`, `φ`, upper-case versions, and LaTeX commands like `\theta`.

### Math vs Physics conventions

Choose with the **Math / Physics** buttons in the settings. The legend at the bottom of the graph always says which angle is which.

| | Math (default) | Physics |
|---|---|---|
| Angle around the z-axis, from +x | θ | φ |
| Angle down from +z | φ | θ |
| Cylindrical radius | r | ρ |
| Spherical radius | ρ | r |

### Overriding detection

Surfaces and solids have a menu (*Auto-detect*, *Cartesian*, *Cylindrical*, *Spherical*) under the line. Pick a system to force it.

---

## 5. Surfaces

### Explicit surfaces

Put one coordinate alone on one side:

```
z = sin(x)cos(y)          Cartesian: z as a function of x, y
x = y² − z²               any Cartesian variable works
r = 2 + 0.6cos(4θ)        cylindrical: radius as a function of θ, z
z = cos(2r) − 2           cylindrical: height as a function of r, θ
θ = π/4                   a half-plane
ρ = 2 + 0.4sin(3θ)sin(2φ) spherical: radius as a function of θ, φ
φ = π/6                   a cone
```

If you leave out the `=`, the expression is read as the height (Cartesian or cylindrical) or the radius (spherical). For example, `x² + y²` alone draws z = x² + y².

### Implicit surfaces

Any other equation is drawn as the surface where both sides are equal:

```
x² + y² + z² = 9
(r − 3)² + z² = 1                  a torus
sin x cos y + sin y cos z + sin z cos x = 0   a gyroid
x² + y² = z²                       a double cone
```

### How surfaces look

- Surfaces are slightly see-through, so you can see parts behind them. Both the front and the back of every surface are drawn.
- Explicit surfaces have faint grid lines on them.
- Everything is cut off at the edges of the graph box. Change the box size with **Scale**.

---

## 6. Solids from inequalities

Use `<`, `>`, `≤` or `≥` to fill a region. Solids are drawn see-through with solid border lines where the region ends, flat caps where the graph box cuts through them, and faint horizontal slices so curved edges are easy to read.

```
z ≤ 3 − (x² + y²)/4                 under a paraboloid
1 < r < 3                           chained inequalities: a thick tube
ρ ≤ 3, φ ≤ π/6                      ice-cream cone (comma = "and")
2 ≤ ρ ≤ 3 and y ≥ 0                 half of a thick shell
1 ≤ r ≤ 3, θ ≤ 3π/2, −1 ≤ z ≤ 1     cylindrical wedge
```

Join several conditions with commas, `and` or `;`. The solid is where they're all true.

---

## 7. Curves, parametric surfaces and points

Write a point with brackets: `(x, y, z)`.

| You write | You get |
|---|---|
| `(1, 2, 3)` | A point. |
| `(3cos t, 3sin t, t/4)` | A curve. `t` is the parameter. |
| `((3 + cos v)cos u, (3 + cos v)sin u, sin v)` | A surface. `u` and `v` are the parameters. |
| `(cos t, sin t)` | A two-entry point or curve lies in the xy-plane. |

Under each curve or surface are range boxes such as **t from [0] to [2π]**. The defaults are t from 0 to 2π, u from 0 to 2π and v from 0 to π. The boxes accept expressions like `-4π` or `a/2`.

---

## 8. Sliders and constants

- **Any unknown letter** in a graph shows a button such as **+ Add slider for a**. Click it to create `a = 1` on a new line.
- **`a = 1`** (a plain number) is a **slider**:
  - Drag it, or type the minimum and maximum in the boxes at its ends. The default range is −10 to 10, and it widens itself if you type a value outside it.
  - **▶** animates it back and forth between the minimum and maximum. **❚❚** pauses.
- **`b = a + 1`** (a formula) is a **constant**. Its chip shows its current value. Constants can use sliders and other constants, in any order.
- Names can have subscripts (`a_1`) or be Greek letters (`α`, `λ`, …).
- A name can only be defined once. A second definition says "*is defined twice*".

---

## 9. The calculator

A line with no variables is a calculation:

```
1+1          = 2
2^10         = 1024
sin(π/6)     = 0.5
3/7 + 1/3    = 0.761904761905
1+1 =        a trailing "=" is fine
```

- Press **a/b** next to the answer to show it as a fraction: 3/7 + 1/3 shows **16/21**. Press it again to go back to the decimal.
- If the answer can't be written exactly as a fraction (for example √2 or π, or anything needing a denominator over 10,000,000), it says ***Can't be written as a fraction — showing the decimal.***
- Calculations can use sliders and constants: with `a = 3`, the line `a² + 1` shows `= 10`.
- Very small answers, and very large answers that aren't whole numbers, use scientific notation, like 9.09494701773 × 10⁻¹³ for `2^(-40)`.

---

## 10. Sets (set-builder notation)

Type `{` (or use the **{ }** key) and write `{ point : conditions }`.

### Sets in space

The point before the colon says which coordinates the set uses:

```
{(x, y, z) : x² + y² + z² = 1, z ≥ 0}        upper hemisphere
{(r, θ, z) : r = 2, 0 ≤ z ≤ 3}                a piece of cylinder
{(ρ, θ, φ) : ρ ≤ 2, φ ≤ π/4}                  a solid cone
{(x, y, z) ∈ ℝ³ : z = xy}                     "∈ ℝ³" is allowed and ignored
```

- **One equation plus inequalities:** the surface, trimmed to where the inequalities hold.
- **Only inequalities:** a solid, as in [section 6](#6-solids-from-inequalities).
- A set can have at most one equation.

### Sets with any letters

If the letters before the colon aren't coordinates, they're read as Cartesian x, y, z (or x, y), and a note says so:

```
{(a, b, c) : a² + b² + c² = 1}     → "(a, b, c) read as Cartesian (x, y, z)"
{(a, b) : a² + b² ≤ 4}             → a disk in the xy-plane
```

### Sets in the plane

Two coordinates give a set drawn flat in the xy-plane:

```
{(x, y) : x < 2}                    a half-plane
{(x, y) : x² + y² = 4}              a circle
{(r, θ) : r ≤ 1 + cos θ}            a filled cardioid
{(x, y) : y ≥ x², y ≤ 2}            a region between curves
```

Regions are filled and outlined. Equations are drawn as bold curves.

### Parametric sets

Put a parametrised point before the colon, and give each parameter's range after it:

```
{(cos t, sin t, t) : t ∈ [0, 4π]}
{(u cos v, u sin v, u) : 0 ≤ u ≤ 2, 0 ≤ v ≤ 2π}
```

### Unions and intersections

Join sets with **∪** and **∩**. Use the keypad, or type `cup` or `cap`. The sides can be sets written out, names of sets, or plain graphs:

```
A = {(x, y, z) : x² + y² + z² ≤ 4}
B = {(x, y, z) : z ≥ 0}
A ∩ B                                  the upper half of the ball
A ∪ B                                  the ball and the half-space, as one solid
{(x, y, z) : x² + y² + z² = 4} ∩ {(x, y, z) : z = 1}      a circle
z = 0 ∩ x = 0                          the y-axis: plain graphs work too
(1, 0, 0) ∩ A                          the point, if it's in A
```

∩ binds tighter than ∪, so `A ∪ B ∩ C` means `A ∪ (B ∩ C)`. Use brackets to group, like `(A ∪ B) ∩ C`.

What you get depends on what meets what:

| Sets | Drawn as |
|---|---|
| solid ∩ solid, solid ∪ solid | one solid, with no walls inside it (the same for regions of the plane) |
| anything ∩ a solid | the part inside the solid: a trimmed surface, a piece of a curve, … |
| surface ∩ surface | the curve where they meet |
| curve ∩ surface | the points where they meet, with a count in the note |
| curve ∩ curve, in the plane | the points where they meet |
| point ∩ anything | the point, if it's in the set, otherwise nothing and a note |
| anything else joined by ∪ | each piece drawn as it is, in the line's colour |

- To find where two surfaces meet, at least one has to be given by an equation, like `z = x²` or `x² + y² + z² = 4`. The other can be anything, even a parametric surface. A curve has to meet a surface given by an equation. In the plane, one of two curves needs an equation.
- If two surfaces are the same, or a curve lies on a surface, you get the surface or the curve itself, and the note says so.
- Points where a curve only touches a surface, without crossing it, are found too. The note counts the points inside the graph box and says how many are outside it.
- A set in the plane can't be joined to a set in space. Write both with (x, y, z), or both with (x, y).
- Two curves in space can't be intersected yet. A solid moved by a function or a matrix can be joined with ∪, but not intersected.
- Functions work on the result: `f(A ∪ B)` draws f(A) and f(B), and `f(A ∩ B)` trims first, then maps. A function that gives a number colours the result, like `k(A ∩ B)`.
- Names can be used before the line that defines them: `C = A ∪ B` can come first.

### Converting between coordinate systems

Sets written in coordinates have **Convert to** buttons, e.g. **Convert to Cartesian | Cylindrical** for a spherical set. Clicking one adds a new line with the same set in the other system, simplified where possible:

```
{(ρ, θ, φ) : ρ = 2}   →   {(x, y, z) : x² + y² + z² = 4}
```

---

## 11. Matrices

### Making a matrix

Type `A = Matrix` on a line. It turns into an editable **3 × 3** identity matrix with `A =` in front.

- **Edit an entry:** click it and type. Entries can be numbers or formulas using sliders and `t`, e.g. `cos(a)`.
- **Resize:** drag the small handle at the bottom-right corner. The size shows while you drag. Or focus the handle and use the arrow keys. Sizes go from 1 × 1 up to 6 × 6.
- **Rename:** click the name in front of `=`.
- A bad entry is outlined in red, with a message saying which row and column.

### Using matrices

```
A(1, 2, 3)               a point: A times a vector
A(cos t, sin t, 0)       a curve, transformed by A
A B (1, 0, 0)            products of matrices
A^2 (1, 1, 1)            powers of square matrices
```

The app checks sizes. For example, *"A 3×3 matrix needs a vector with 3 entries, not 2."*

### Applying a matrix to a set

Put the matrix directly in front of a set to transform every point of it:

```
A{(x, y, z) : x² + y² + z² = 1}       the unit sphere, mapped by A
A{(x, y) : x² + y² ≤ 1}               a 2 × 2 (or 3 × 3) matrix on a planar set
```

Tick **Show both** to draw the original set in a second colour next to the transformed one. The colour key appears beside the checkbox.

---

## 12. Functions

### Defining a function

Write a name, its inputs in brackets, `=`, and what it gives:

```
f(a, b, c) = (3a, 2b, 4c)        ℝ³ → ℝ³
g(u, v) = (u, v, u² − v²)        ℝ² → ℝ³
m(x, y) = x + y                  ℝ² → ℝ
q(x) = x²                        ℝ → ℝ
```

- The chip shows the detected input and output spaces, e.g. **Function ℝ³ → ℝ³**.
- The *reads as* line shows the rule, e.g. *(a, b, c) ↦ (3a, 2b, 4c)*, and says whether it takes and gives Cartesian points or numbers.
- Inputs can be any letters, including x, y, z.
- A function may use sliders, e.g. `f(a, b, c) = (ka, b, c)`. Moving `k` redraws everything that uses `f`.
- Functions can call other functions. A function can't call itself.
- A line like `a(x) = z` uses a coordinate that isn't one of its inputs, so it's read as an ordinary equation (a·x = z), not a function.
- Once `f` is defined, a line like `f(x, y, z) = 4` (coordinates in, a number or slider out) is the equation f = 4: the level surface, drawn like any implicit surface.

### Drawing a function

A function line draws itself. What you see depends on how many numbers go in (n) and come out (m):

| f : ℝⁿ → ℝᵐ | Drawn as | Other view in the menu |
|---|---|---|
| ℝ → ℝ, `q(x) = x²` | its graph y = q(x), in the xy-plane | |
| ℝ → ℝ², `g(t) = (cos t, sin 2t)` | the curve it traces, in the xy-plane | Graph: the space curve (t, g₁(t), g₂(t)) |
| ℝ → ℝ³, `h(t) = (cos t, sin t, t/4)` | the curve it traces | |
| ℝ² → ℝ, `m(x, y) = x² − y²` | its graph z = m(x, y) | Level curves m = c in the xy-plane |
| ℝ² → ℝ², `F(x, y) = (−y, x)` | arrows: F(p) drawn at each point p | Grid image: where F sends a grid of lines |
| ℝ² → ℝ³, `s(u, v) = (u, v, u² − v²)` | the surface it traces | |
| ℝ³ → ℝ, `f(x, y, z) = x² + y² + z²` | level surfaces f = c | |
| ℝ³ → ℝ², `p(x, y, z) = (x² + y², z)` | fibers: the curves where p = (c₁, c₂) | Arrows (p₁, p₂, 0) |
| ℝ³ → ℝ³, `F(x, y, z) = (−y, x, z/2)` | arrows | Grid image |

- **Picking a view:** when there's a choice, a menu next to the chip switches between them. For ℝ² → ℝ² and ℝ³ → ℝ³ the default is arrows when the inputs are the coordinates themselves, like `F(x, y)`, and the grid image when they aren't, like the polar map `P(r, θ) = (r cos θ, r sin θ)`, whose grid image is circles and rays.
- **Domains:** graphs, arrows and level sets cover the graph box. Curves, surfaces and grid images have range boxes for each input. Left blank, an input used inside sin or cos runs over a full turn, 0 to 2π (0 to π for the angle down from +z when the angle around z is an input too), an `r` or `ρ` runs from 0 to the box edge, and anything else spans the box. The greyed text shows the default. Sliders work in these boxes.
- **Levels:** level curves and level surfaces pick round values across the function's range. Their legend shows each level's colour, from light (low) to dark (high), flipped in dark mode. Type your own in the **levels** box, like `-1, 0, 1`, `1 4 9` or `0, c` with a slider c. A function that's constant in the box says so instead.
- **Arrows** keep their length scale while a slider moves, so you can watch the field grow and shrink. The note says the scale, for example *arrows at 0.05× true length*, and how many very long arrows were shortened to fit. Where the field is about zero there's a dot.
- **Helpers start hidden.** A function that another line uses, like `f` in `f(A)`, isn't drawn at first: its dot is hollow and a note says so. Click the dot to draw it.
- Poles are never drawn as surfaces: for `1/(1 − x² − y² − z²)` the level surfaces stop short of the unit sphere instead of drawing a fake sheet on it.
- Functions with more than three inputs can't be drawn.

### Using functions in any line

```
f(1, 2, 3)              a point: (3, 4, 12)
f(cos t, sin t, t)      a curve
z = m(x, y)             a surface
q(3)                    a calculation: = 9
```

### Applying a function to a set

Give `f` a set and it draws the image of that set, meaning every point of the set sent through `f`:

```
f({(a, b, c) : a² + b² + c² = 1})       an ellipsoid with semi-axes 3, 2, 4
g({(x, y) : x² + y² ≤ 4})               a disk lifted into a saddle surface
```

A function that gives a single number can't move points, so it shows its values instead:

```
m(x, y) = x² − y²
m({(x, y) : x² + y² ≤ 4})               the graph of m over the disk: a saddle patch

k(x, y, z) = z
k({(x, y, z) : x² + y² + z² = 4})       the sphere, coloured by k
```

- **On a set in the plane** you get the graph of the function over the set: each point (x, y) is lifted to height m(x, y). **Show both** keeps the flat set too.
- **On a set in space** the set keeps its shape and is coloured by the value: light for low values, dark for high (the other way round in dark mode), with thin lines at round values. A legend shows the range. When a few far-out values would squash the colours, they stop at the 5th and 95th percentiles (≤ and ≥ in the legend) and the note gives the full range. For a solid, the colour shows the values on its surface.
- If the function is the same all over the set, the whole set gets one colour and the note gives the value, like *q ≈ 4 all over this set* for x² + y² + z² on the sphere of radius 2.
- Where the function isn't defined, like √z below the xy-plane, the set is grey.
- If it divides by zero along part of the set, like `1/z` on a sphere, the colours stop at the 5th and 95th percentiles and the note says it's unbounded there.
- If it blows up all over the set, for example `1/(1 − x² − y² − z²)` on the unit sphere, where it divides by zero everywhere, the set isn't coloured and the line says why. The same happens when it changes too fast for the drawn mesh, like `sin(10x)` on a big sphere, and the message suggests raising **Resolution**.
- On a set in space, a function that gives a number has to be the last one applied: `g(k(S))` says so. A graph over a planar set is an ordinary surface in space, so it can be mapped further, like `g(m(D))`.

### Naming sets

Give a set a name on its own line, then use the name:

```
A = {(a, b, c) : a² + b² + c² = 1}
f(A)
C = f(A)          results can be named too
h(f(A))           and functions can be chained
```

A named set is also drawn on its own line, and you can hide it with its dot.

Applying a function works with surfaces, solids, planar regions and curves, with parametric sets, and with unions and intersections of sets (see [Unions and intersections](#unions-and-intersections)). **Show both** draws the original set next to its image.

### Checks: dimensions and coordinate systems

The app checks that the set and the function fit together, and explains when they don't:

- **Wrong dimension:** *"f : ℝ³ → ℝ³ takes 3 inputs, but A is in ℝ², with points (a, b)."*
- **After a function that gives a number:** *"k already turns this set into numbers (its colours), so g can't be applied after it."*
- **Undefined function:** *"h isn't a function yet — define it on another line, like h(x, y, z) = (…, …, …)."*

Functions work on **Cartesian** points. If the set is written in cylindrical, spherical or polar coordinates, the line says so:

> *A is written in spherical coordinates (ρ, θ, φ), but f works on Cartesian points (x, y, z).*

Click **Make a Cartesian copy and use it** to fix it:

- **Named set** (`f(A)`): a new line `A_c = {(x, y, z) : …}` is added under A with the same set in Cartesian coordinates, and your line changes to `f(A_c)`. The original A is kept.
- **Set written inside the brackets** (`f({(ρ, θ, φ) : …})`): a new line `S_1 = {(x, y, z) : …}` is added, and your line changes to `f(S_1)`.

### Good to know

- Curves and parametric surfaces are mapped exactly. Surfaces and solids are reshaped point by point from their drawn mesh, so a function that stretches a shape a lot can look slightly faceted. Raising **Resolution** helps.
- Only the part of the set inside the graph box is mapped.

---

## 13. Sequences

### Writing a sequence

```
seq(k)(1/k, 1/(3k), 1/(2k))
```

- The first bracket names the index. It can be any letter: `k`, `n`, `θ`, even `x`.
- The second bracket is the term. With three entries it's a point in space, with two it's a point in the xy-plane, and with one it's a number on the x-axis.
- The terms can use sliders, other constants, functions and matrices: `seq(k)(A(1/k, 1, 0))`.

### Which terms

Under the line: **k from [1] to [50]**.

- Both ends accept numbers or expressions, including sliders, e.g. `1` to `N`. Only whole-number values of k are used.
- Press **∞** to make the sequence go on forever. The end box shows ∞, and the chip says *k → ∞*. Press **∞** again to return to your previous end value. Typing `∞`, `inf` or `infinity` in the box also works.
- "Forever" computes the first 100,000 terms. Where terms land on top of each other, only one dot is drawn, so a convergent sequence piles up neatly at its limit. Terms outside the graph box are skipped.
- A finite range can have up to 100,000 terms, and the app draws at most 20,000 separate dots. A note tells you if either limit is reached.

### How it looks

- One small dot per term, in the line's colour. The **first term is a bigger dot**, so you can see where the sequence starts.
- A thin line joins the terms in order: 1 → 2 → 3 → … Untick **Connect the dots** to hide it. If a term is undefined, like n = 3 in `1/(n − 3)`, the line breaks there.

### Messages

- *"The terms don't use k — every dot would land in the same place."*
- *"Inside seq only k changes — found x. Use a slider instead."*
- *"The range for k has no whole numbers in it."*

---

## 14. Moving around: Orbit mode

Orbit is the default camera.

| Action | Mouse | Touch |
|---|---|---|
| Rotate | Drag | Drag with one finger |
| Pan | Right-drag | Drag with two fingers |
| Zoom (change the box size) | Scroll, when **Scroll to zoom** is ticked | The **Scale** slider |
| Start over | **Reset view** | **Reset view** |

Scrolling changes the **Scale**, the size of the graph box, rather than moving the camera, so the axes and grid always stay neat. The box goes from ±0.5 to ±1000.

---

## 15. Fly mode

Click **Fly** in the settings to turn your graph into a 3D world you can move through.

### Controls

| Action | Keys | Touch |
|---|---|---|
| Look around | Click the graph once, then move the mouse. **Esc** gives the mouse back. | Drag on the graph |
| Forward / back | **W / S** or **↑ / ↓** | **▲ / ▼** buttons |
| Left / right | **A / D** or **← / →** | |
| Up | **Space** or **E** | **Rise** button |
| Down | **Shift** or **Q** | **Sink** button |
| Speed | Scroll (×0.05 to ×20, shown in the legend) | |

A small dot marks the centre of the screen.

### How the world works

- In fly mode the graph has no box. Surfaces and solids carry on in every direction.
- **Render distance** (2 to 1000, replacing the Scale slider) sets how far you can see. Distant objects fade into fog. Changing it never changes the shapes. It only decides how far out they're drawn.
- The world is built in chunks around you, nearest and in-view first. While it builds, the legend shows *building world NN%*. Chunks far away are drawn with less detail.
- **Reset view** puts you back at a comfortable spot near the origin.
- Click **Orbit** to go back to the normal view.

---

## 16. Settings reference

| Setting | Range | What it does |
|---|---|---|
| **Orbit / Fly** | | Camera mode. See sections 14 and 15. |
| **Math / Physics** | | Which angle is θ and which is φ, and which radius is r and which is ρ. See [section 4](#math-vs-physics-conventions). |
| **Scale** (orbit) | ±0.5 to ±1000 | Half-width of the graph box. Snaps to round numbers. |
| **Render distance** (fly) | 2 to 1000 | How far you can see in fly mode. |
| **Scroll to zoom / Scroll sets speed** | on/off | Whether the mouse wheel changes the scale (orbit) or the flying speed (fly). |
| **Resolution** | ×0.5 to ×3 | How finely surfaces, solids and curves are sampled. Higher means smoother edges but slower drawing. |

The app follows your system's light or dark mode.

---

## 17. Reference: functions, constants and operators

### Functions

| Kind | Functions |
|---|---|
| Trigonometric | `sin cos tan sec csc cot` |
| Inverse trig | `arcsin arccos arctan` (or `asin acos atan`), `atan2(y, x)` |
| Hyperbolic | `sinh cosh tanh`, `arcsinh arccosh arctanh` |
| Roots and powers | `sqrt` (√), `cbrt`, `nthRoot(x, n)`, `exp`, `pow(a, b)` |
| Logarithms | `ln` (natural log), `log` (base 10), `log2`, `log(x, b)` (base b) |
| Rounding and sign | `abs` (or `|x|`), `floor`, `ceil`, `round`, `sign` / `sgn` |
| Other | `min`, `max`, `mod(a, b)` (or `a mod b`), `n!` |

### Constants

`π` (`pi`), `e`, `τ` (`tau` = 2π).

### Operators

`+ − × ÷`, `^` for powers, implied multiplication, `!` for factorials, `mod` for remainders, `|…|` for absolute value, `= < > ≤ ≥`, and `∪ ∩` between sets.

### Reserved names

| Name | Meaning |
|---|---|
| `x y z` | Cartesian coordinates |
| `r ρ θ φ` | Cylindrical and spherical coordinates |
| `t` | Curve parameter |
| `u v` | Surface parameters |
| `seq` | Sequences |
| `Matrix` | `A = Matrix` makes a matrix |

Any other name, like `a`, `k`, `N`, `a_1` or `λ`, can be a slider, constant, matrix, function or set.

---

## 18. Messages and troubleshooting

| You see | What to do |
|---|---|
| ***Nothing to draw inside the current range.*** | The shape is outside the graph box, or too small to see at this scale. Change **Scale**, or raise **Resolution** for very thin shapes. |
| ***a isn't defined yet.*** + **Add slider for a** | Click the button, or define `a` on another line. |
| ***Something is missing on one side of the =.*** | Finish the equation. |
| ***Add an = sign so I know what to solve for.*** | The expression contains the coordinate it would be solved for. Write it as an equation. |
| ***Mixed coordinates need an equation.*** | When mixing Cartesian and polar variables, write `… = …`. |
| ***… is defined twice.*** | Rename or delete one of the definitions. |
| ***A set can have one equation…*** | Keep one equation and trim it with inequalities. Or intersect two sets: `{…: x² + y² + z² = 4} ∩ {…: z = 1}`. |
| ***To find where two surfaces meet, one of them has to be given by an equation…*** | Write one of the surfaces as an equation, like `z = …`, instead of as a parametrisation. |
| ***B isn't a set yet…*** | Define `B` on another line, like `B = {(x, y, z) : …}`. |
| ***… is a set in the plane and … is in space…*** | Write both sets with (x, y, z), or both with (x, y). |
| ***they don't meet*** (in the note) | The sets don't meet inside the graph box. Try a larger **Scale**. |
| ***f blows up on this set…*** | The function divides by zero all over the set, so colouring the set by it wouldn't mean anything. Try a set that avoids the problem, or draw the function's own level surfaces. |
| ***f changes too fast for the mesh here…*** | Raise **Resolution**, or look at a smaller set. |
| A function line isn't drawn and its dot is hollow | Another line uses it, so it starts hidden. Click the dot to draw it. |
| Edges look bumpy or jagged | Raise **Resolution**. |
| The app feels slow (low FPS) | Lower **Resolution**, hide graphs you don't need with their dots, or lower the render distance in fly mode. |
| `1e9` doesn't mean a billion | `e` is always Euler's number, so `1e9` reads as 1·e·9. Type `1000000000` instead. |
| Nothing loads, or the page is blank | Check your internet connection. The libraries load from CDNs. |
| Fly mode doesn't respond to the mouse | Click the graph once to capture the mouse. Press **Esc** to release it. |
