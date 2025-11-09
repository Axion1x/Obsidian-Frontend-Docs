## Introduction

In CSS, **units** define the measurement of values like length, size, spacing, or angles.  
Understanding units is crucial for responsive design, typography, and layout.  

Units can be divided into **absolute** and **relative** units.

---

## 1. Absolute Units

Absolute units are fixed and do **not scale** with the viewport or parent elements.  

| Unit | Description | Example |
|------|------------|---------|
| `px` | Pixels, screen pixels | `width: 200px;` |
| `pt` | Points, 1pt = 1/72in | `font-size: 12pt;` |
| `cm` | Centimeters | `margin: 2cm;` |
| `mm` | Millimeters | `margin: 10mm;` |
| `in` | Inches | `width: 1in;` |
| `pc` | Picas, 1pc = 12pt | `margin: 2pc;` |

**Example:**

```css
div.box {
  width: 200px;
  height: 100px;
}
Always exactly 200px wide regardless of parent or screen size.

go
Копіювати код

---

### **Частина 2: Relative Units & Percentages**

```markdown
## 2. Relative Units

Relative units scale depending on the **parent element**, **root font size**, or **viewport**.

| Unit | Relative to | Example |
|------|------------|---------|
| `%` | Parent element size | `width: 50%;` |
| `em` | Font size of current element | `font-size: 2em;` |
| `rem` | Font size of root element (`html`) | `font-size: 1.5rem;` |
| `vw` | 1% of viewport width | `width: 50vw;` |
| `vh` | 1% of viewport height | `height: 100vh;` |
| `vmin` | 1% of smaller viewport dimension | `width: 50vmin;` |
| `vmax` | 1% of larger viewport dimension | `width: 50vmax;` |

**Example:**

```css
p {
  font-size: 2em; /* twice the parent font size */
}

div.container {
  width: 50vw; /* 50% of viewport width */
}
em scales with parent font size

rem scales with root font size

vw / vh scale with viewport

perl
Копіювати код

---

### **Частина 3: Special Values & Tips**

```markdown
## 3. Special Values

| Value | Description | Example |
|-------|------------|---------|
| `auto` | Let browser calculate value | `margin: auto;` |
| `min-content` | Smallest possible size | `width: min-content;` |
| `max-content` | Largest possible size | `width: max-content;` |
| `fit-content` | Fit content within max size | `width: fit-content(200px);` |
| `calc()` | Mathematical expressions | `width: calc(100% - 50px);` |
| `inherit` | Take value from parent | `color: inherit;` |
| `initial` | Set property to default | `font-size: initial;` |
| `unset` | Resets value to inherit or initial | `margin: unset;` |

**Example:**

```css
div.box {
  width: calc(100% - 20px);
  max-width: 500px;
}
calc() allows combining units (%, px, em, rem)

min-content, max-content useful for flexible layouts