
## Introduction

This section explains how the browser decides **which CSS rule to apply** when an element matches multiple selectors.  
The three main principles are:

1. **Specificity** — the weight of the selector.  
2. **Cascade** — the order in which rules are applied.  
3. **Inheritance** — properties that are passed from parent elements to children.  

---
## 1. Specificity

Specificity is measured as three numbers `(A, B, C)`:

| Number | What it counts | Example |
|--------|----------------|---------|
| **A**  | ID selectors   | `#main` → 1 |
| **B**  | Classes, attributes, pseudo-classes | `.btn`, `[data-type="main"]`, `:hover` → 1 each |
| **C**  | Elements, pseudo-elements | `p`, `div`, `::before` → 1 each |

**Inline styles** (`style="..."`) have the highest specificity `(1,0,0,0)`.

**!important** does not change specificity but makes a rule override all normal rules.  
If two rules have `!important`, specificity `(A,B,C)` is used to decide.

---

### 1.1 Basic selector examples

```css
p { color: blue; }             /* (0,0,1) */
.text { color: red; }          /* (0,1,0) */
#main { color: green; }        /* (1,0,0) */
```

- `<p class="text" id="main">` → **#main** wins (green).

```css
.text[data-type="main"] { color: blue; } /* (0,2,0) */ 
p.highlight { color: green !important; } /* (0,1,1) + !important */
```

- `!important` elevates `p.highlight` above others → **green**.

```css
p::before { content:"*"; }       /* (0,0,1) */ 
p:hover::before { color:red; }   /* (0,1,2) */
```

- `:hover` pseudo-class → B+1
- `::before` pseudo-element → C+1
## 2. Cascade

1. Check `!important` first.
    
2. If multiple `!important` rules exist, compare specificity `(A,B,C)`.
    
3. If specificity is the same, the **last rule in CSS wins**.
    

---

## 3. Inheritance

- Some properties, like `color` or `font-family`, inherit from parent elements.
    
- Other properties, like `margin` or `padding`, **do not inherit**.
    
- Inheritance is applied **after specificity and cascade**, so explicit rules override inherited ones.
    

---

## 4. Summary Table of Specificity

| Selector type  | Example                | Specificity            | Notes                                   |
| -------------- | ---------------------- | ---------------------- | --------------------------------------- |
| ID             | `#main`                | (1,0,0)                | Strongest standart selector             |
| Class          | `.btn`                 | (0,1,0)                |                                         |
| Attribute      | `[data-id="x"]`        | (0,1,0)                | Counts as a class                       |
| Pseudo-class   | `:hover`               | (0,1,0)                | Counts as a class                       |
| Element        | `p`, `div`             | (0,0,1)                |                                         |
| Pseudo-element | `::before`             | (0,0,1)                | Counts as an element                    |
| Combined       | `#id.class:pseudo`     | Depends on composition | All values summed                       |
| Inline         | `<p style="...">`      | (1,0,0,0)              | Stronger than any CSS selector          |
| !important     | `color:red !important` | Overrides normal rules | If two !important → compare specificity |

---

## 5. Combined Selector Examples

```css
p.text[data-type="main"] { color: blue; } /* (0,2,1) */ 
#intro { color: red; }                     /* (1,0,0) */ 
p.highlight { color: green !important; }  /* (0,1,1) + !important */`
```
- `!important` elevates `p.highlight` above others.
- `#intro` without `!important` is stronger than `.text[data-type="main"]`, but loses to `p.highlight` because of `!important`.