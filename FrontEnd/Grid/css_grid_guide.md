# 📊 CSS Grid Complete Guide

**Simple and Easy to Understand with Clear Examples**

---

## 🎯 What is CSS Grid?

CSS Grid Layout is a **two-dimensional layout system** for the web. It lets you lay out content in rows and columns, making it easier to design web pages without having to use floats and positioning.

> **Key Advantage:** Unlike Flexbox which is one-dimensional (either row or column), Grid works with both rows and columns simultaneously!

---

## 1. Basic Grid Setup

To create a grid, set `display: grid` on the parent container and define columns using `grid-template-columns`.

### Syntax:
```css
.grid-container {
  display: grid;
  grid-template-columns: 200px 200px 200px;
  gap: 10px;
}
```

### Explanation:
- Creates 3 columns, each 200px wide
- 10px gap between items

### HTML Example:
```html
<div class="grid-container">
  <div class="item">Item 1</div>
  <div class="item">Item 2</div>
  <div class="item">Item 3</div>
</div>
```

---

## 2. Fractional Units (fr)

The `fr` unit represents a **fraction of the available space** in the grid container.

### Syntax:
```css
.grid-container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
  gap: 10px;
}
```

### Explanation:
- The middle column takes twice as much space as the other columns
- Total = 4fr (1+2+1), so middle column gets 2/4 (50%) of space
- First column: 25%, Middle column: 50%, Last column: 25%

### Visual Representation:
```
┌─────────┬──────────────────┬─────────┐
│   1fr   │       2fr        │   1fr   │
│  Item 1 │     Item 2       │ Item 3  │
└─────────┴──────────────────┴─────────┘
```

---

## 3. repeat() Function

Instead of writing the same value multiple times, use `repeat()`.

### Syntax:
```css
/* Instead of: 1fr 1fr 1fr */
.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}
```

### Explanation:
- `repeat(3, 1fr)` creates 3 equal columns
- Items automatically wrap to new rows
- Much cleaner and easier to maintain

### Other Examples:
```css
/* 4 equal columns */
grid-template-columns: repeat(4, 1fr);

/* 3 columns: 100px each */
grid-template-columns: repeat(3, 100px);

/* Mixed pattern repeated */
grid-template-columns: repeat(2, 1fr 2fr);  /* Creates: 1fr 2fr 1fr 2fr */
```

---

## 4. Grid Rows

Control row heights with `grid-template-rows`.

### Syntax:
```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 100px 150px;
  gap: 10px;
}
```

### Explanation:
- First row is 100px tall
- Second row is 150px tall
- Additional rows will auto-size based on content

### Example:
```html
<div class="grid-container">
  <div>Row 1, Col 1 (100px tall)</div>
  <div>Row 1, Col 2 (100px tall)</div>
  <div>Row 1, Col 3 (100px tall)</div>
  <div>Row 2, Col 1 (150px tall)</div>
  <div>Row 2, Col 2 (150px tall)</div>
  <div>Row 2, Col 3 (150px tall)</div>
</div>
```

---

## 5. Grid Gap (Gutter)

Create space between grid items using `gap`, `row-gap`, or `column-gap`.

### Syntax:
```css
/* Shorthand for both row and column gap */
.grid-container {
  gap: 20px;
}

/* Or specify separately */
.grid-container {
  row-gap: 20px;
  column-gap: 10px;
}

/* Old syntax (still supported) */
.grid-container {
  grid-gap: 20px;
  grid-row-gap: 20px;
  grid-column-gap: 10px;
}
```

### Explanation:
- `gap: 20px` - 20px gap between all items (both rows and columns)
- `row-gap: 20px` - 20px gap between rows only
- `column-gap: 10px` - 10px gap between columns only

---

## 6. Grid Template Areas

Create named grid areas for more **semantic and readable** layouts.

### Syntax:
```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-areas:
    "header header header"
    "sidebar main main"
    "footer footer footer";
  gap: 10px;
}

.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }
.footer  { grid-area: footer; }
```

### HTML Example:
```html
<div class="grid-container">
  <header class="header">Header</header>
  <aside class="sidebar">Sidebar</aside>
  <main class="main">Main Content</main>
  <footer class="footer">Footer</footer>
</div>
```

### Visual Layout:
```
┌─────────────────────────────────────┐
│              Header                 │
├───────────┬─────────────────────────┤
│  Sidebar  │   Main Content          │
│           │                         │
├───────────┴─────────────────────────┤
│              Footer                 │
└─────────────────────────────────────┘
```

### Use a dot (.) for empty cells:
```css
grid-template-areas:
  "header header header"
  "sidebar main ."
  "footer footer footer";
```

---

## 7. Spanning Columns and Rows

Make items span multiple columns or rows using `grid-column` and `grid-row`.

### Syntax:
```css
.item-span-col {
  grid-column: span 2;  /* Spans 2 columns */
}

.item-span-row {
  grid-row: span 2;     /* Spans 2 rows */
}

.item-span-both {
  grid-column: span 2;
  grid-row: span 2;
}
```

### Complete Example:
```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

.featured {
  grid-column: span 2;  /* Takes 2 columns */
  grid-row: span 2;     /* Takes 2 rows */
}
```

### HTML:
```html
<div class="grid-container">
  <div class="featured">Featured Item (2x2)</div>
  <div>Item 2</div>
  <div>Item 3</div>
  <div>Item 4</div>
  <div>Item 5</div>
</div>
```

### Alternative Syntax (using line numbers):
```css
.item {
  grid-column: 1 / 3;   /* Start at line 1, end at line 3 (spans 2 columns) */
  grid-row: 2 / 4;      /* Start at line 2, end at line 4 (spans 2 rows) */
}

/* Or mix span with line numbers */
.item {
  grid-column: 1 / span 2;  /* Start at line 1, span 2 columns */
}
```

---

## 8. Grid Alignment

Align items within their grid cells and align the entire grid within the container.

### Item Alignment (within cells):

```css
.grid-container {
  display: grid;
  
  /* Align items vertically (column axis) */
  align-items: center;  /* center | start | end | stretch */
  
  /* Align items horizontally (row axis) */
  justify-items: center;  /* center | start | end | stretch */
}
```

### Grid Alignment (entire grid within container):

```css
.grid-container {
  display: grid;
  height: 500px;
  
  /* Align entire grid vertically */
  align-content: center;  /* center | start | end | space-between | space-around | space-evenly */
  
  /* Align entire grid horizontally */
  justify-content: center;  /* center | start | end | space-between | space-around | space-evenly */
}
```

### Individual Item Alignment:

```css
.item {
  align-self: end;     /* Override align-items for this item */
  justify-self: start; /* Override justify-items for this item */
}
```

### Quick Reference:
| Property | Axis | What it aligns |
|----------|------|----------------|
| `align-items` | Vertical (column) | Items within their cells |
| `justify-items` | Horizontal (row) | Items within their cells |
| `align-content` | Vertical (column) | Entire grid |
| `justify-content` | Horizontal (row) | Entire grid |
| `align-self` | Vertical (column) | Individual item |
| `justify-self` | Horizontal (row) | Individual item |

---

## 9. Responsive Grids (auto-fit / auto-fill)

Create responsive grids that **automatically adjust** column count based on available space.

### auto-fit Syntax:
```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 10px;
}
```

### auto-fill Syntax:
```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  gap: 10px;
}
```

### Explanation:

**`minmax(150px, 1fr)`:**
- Each column is **minimum 150px**
- Maximum size is **1fr** (fills available space)

**`auto-fit`:**
- Fits columns into available space
- **Collapses empty tracks** and expands existing columns

**`auto-fill`:**
- Fills the row with as many columns as possible
- **Keeps empty tracks** (ghost columns)

### Difference between auto-fit and auto-fill:

```css
/* With 3 items in a 1000px container */

/* auto-fit: Items will expand to fill the full width */
repeat(auto-fit, minmax(200px, 1fr))
/* Result: 3 columns at ~333px each */

/* auto-fill: Creates ghost columns, items stay at 200px */
repeat(auto-fill, minmax(200px, 1fr))
/* Result: 5 columns total (3 with content, 2 empty) */
```

### Practical Example (Responsive Image Gallery):
```css
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}

.gallery img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
```

---

## 10. Grid Line Positioning

Position items using **grid line numbers**. Grid lines are numbered starting from 1.

### Understanding Grid Lines:

For a 3-column grid:
```
Line 1   Line 2   Line 3   Line 4
  |        |        |        |
  | Col 1  | Col 2  | Col 3  |
  |        |        |        |
```

### Syntax:
```css
.item {
  grid-column-start: 1;
  grid-column-end: 3;   /* Spans from line 1 to 3 (2 columns) */
  
  grid-row-start: 2;
  grid-row-end: 4;      /* Spans from line 2 to 4 (2 rows) */
}

/* Shorthand */
.item {
  grid-column: 1 / 3;   /* Start / End */
  grid-row: 2 / 4;
}

/* Using span */
.item {
  grid-column: 1 / span 2;  /* Start at line 1, span 2 columns */
  grid-row: 2 / span 2;     /* Start at line 2, span 2 rows */
}

/* Span from current position */
.item {
  grid-column: span 2;  /* Span 2 columns from auto-placed position */
}
```

### Negative Line Numbers:

```css
.item {
  grid-column: 1 / -1;  /* From first line to last line (full width) */
  grid-row: 2 / -2;     /* From line 2 to second-to-last line */
}
```

> **Remember:** Grid lines are numbered starting from **1, not 0**. A 3-column grid has **4 vertical lines** (1, 2, 3, 4).

---

## 11. Implicit vs Explicit Grid

### Explicit Grid:
Rows and columns you **define** with `grid-template-rows` and `grid-template-columns`.

```css
.grid-container {
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 100px 200px;
}
```

### Implicit Grid:
Rows and columns **automatically created** when you place more items than fit in the explicit grid.

```css
.grid-container {
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 100px;
  
  /* Control size of implicit rows */
  grid-auto-rows: 150px;
  
  /* Control size of implicit columns */
  grid-auto-columns: 200px;
  
  /* Control flow direction */
  grid-auto-flow: row;  /* row | column | dense */
}
```

### grid-auto-flow values:
- `row` (default): Fill rows first, create new rows as needed
- `column`: Fill columns first, create new columns as needed
- `dense`: Try to fill holes in the grid (can change visual order)

---

## 📚 Quick Reference Summary

### Container Properties:

| Property | Description |
|----------|-------------|
| `display: grid` | Creates a grid container |
| `grid-template-columns` | Define column sizes |
| `grid-template-rows` | Define row sizes |
| `grid-template-areas` | Define named grid areas |
| `grid-template` | Shorthand for rows/columns/areas |
| `gap` | Space between items (row and column) |
| `row-gap` | Space between rows |
| `column-gap` | Space between columns |
| `justify-items` | Align items horizontally within cells |
| `align-items` | Align items vertically within cells |
| `justify-content` | Align entire grid horizontally |
| `align-content` | Align entire grid vertically |
| `grid-auto-rows` | Size of implicit rows |
| `grid-auto-columns` | Size of implicit columns |
| `grid-auto-flow` | How auto-placed items flow |

### Item Properties:

| Property | Description |
|----------|-------------|
| `grid-column` | Column position/span (shorthand) |
| `grid-row` | Row position/span (shorthand) |
| `grid-column-start` | Starting column line |
| `grid-column-end` | Ending column line |
| `grid-row-start` | Starting row line |
| `grid-row-end` | Ending row line |
| `grid-area` | Named area or shorthand for row/column |
| `justify-self` | Individual item horizontal alignment |
| `align-self` | Individual item vertical alignment |

### Common Units:

| Unit | Description |
|------|-------------|
| `fr` | Fraction of available space |
| `px` | Fixed pixels |
| `%` | Percentage of container |
| `em/rem` | Relative to font size |
| `auto` | Automatic sizing |
| `min-content` | Minimum size needed for content |
| `max-content` | Maximum size content can take |
| `minmax(min, max)` | Size range between min and max |

### Useful Functions:

| Function | Description |
|----------|-------------|
| `repeat(count, size)` | Repeat a pattern |
| `minmax(min, max)` | Define size range |
| `auto-fit` | Fit columns (collapse empty tracks) |
| `auto-fill` | Fill columns (keep empty tracks) |
| `fit-content(size)` | Use content size, max at specified size |

---

## 🎓 Common Use Cases & Examples

### 1. **Responsive Image Gallery**

```css
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 15px;
}

.gallery img {
  width: 100%;
  height: 250px;
  object-fit: cover;
  border-radius: 8px;
}

.featured {
  grid-column: span 2;
  grid-row: span 2;
}
```

### 2. **Holy Grail Layout**

```css
.container {
  display: grid;
  grid-template-columns: 200px 1fr 200px;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "header header header"
    "sidebar main ads"
    "footer footer footer";
  min-height: 100vh;
  gap: 10px;
}

.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }
.ads     { grid-area: ads; }
.footer  { grid-area: footer; }
```

### 3. **Card Layout with Different Sizes**

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 200px;
  gap: 20px;
}

.card-large {
  grid-column: span 2;
  grid-row: span 2;
}

.card-wide {
  grid-column: span 2;
}

.card-tall {
  grid-row: span 2;
}
```

### 4. **Centered Content**

```css
.center-container {
  display: grid;
  place-items: center;  /* Shorthand for align-items + justify-items */
  min-height: 100vh;
}

/* Or the longer way */
.center-container {
  display: grid;
  align-items: center;
  justify-items: center;
  min-height: 100vh;
}
```

### 5. **12-Column Grid System**

```css
.grid-12 {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 20px;
}

/* Usage */
.col-6 { grid-column: span 6; }  /* Half width */
.col-4 { grid-column: span 4; }  /* Third width */
.col-3 { grid-column: span 3; }  /* Quarter width */
```

---

## 💡 Pro Tips

### 1. **Use Browser DevTools**
In Chrome/Edge/Firefox, inspect a grid element to see grid overlays showing lines, areas, and gaps visually!

### 2. **Place Items Shorthand**
```css
/* Instead of */
align-items: center;
justify-items: center;

/* Use */
place-items: center;

/* Works for content too */
place-content: center;
```

### 3. **Full-Bleed Layouts**
```css
.full-width {
  grid-column: 1 / -1;  /* Span from first to last line */
}
```

### 4. **Responsive Without Media Queries**
```css
.grid {
  grid-template-columns: repeat(auto-fit, minmax(min(250px, 100%), 1fr));
}
```
This prevents overflow on small screens!

### 5. **Overlapping Elements**
```css
.item-1 { grid-area: 1 / 1 / 2 / 3; }
.item-2 { grid-area: 1 / 2 / 3 / 3; }  /* Overlaps with item-1 */
```
Use `z-index` to control stacking.

---

## 🎓 Practice Exercises

### Exercise 1: Simple Gallery
Create a photo gallery grid that:
- Has 4 columns on large screens
- Automatically adjusts on smaller screens
- Uses 15px gap
- Makes the first item span 2x2

**Solution:**
```css
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 15px;
}

.featured {
  grid-column: span 2;
  grid-row: span 2;
}
```

### Exercise 2: Dashboard Layout
Create a dashboard with:
- Header spanning full width
- 3 equal-width columns below
- Footer spanning full width

**Solution:**
```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-areas:
    "header header header"
    "col1 col2 col3"
    "footer footer footer";
  gap: 20px;
}

.header { grid-area: header; }
.col1   { grid-area: col1; }
.col2   { grid-area: col2; }
.col3   { grid-area: col3; }
.footer { grid-area: footer; }
```

### Exercise 3: Complex Card Layout
Create a card grid where:
- Default cards are 1x1
- Featured card is 2x2 (top-left)
- 2 wide cards (1x2) in the first row

**Solution:**
```css
.cards {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 150px;
  gap: 15px;
}

.featured { grid-column: span 2; grid-row: span 2; }
.wide     { grid-column: span 2; }
```

---

## 🔗 Additional Resources

- [MDN CSS Grid Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout)
- [CSS Tricks Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [Grid by Example](https://gridbyexample.com/)
- [CSS Grid Generator](https://cssgrid-generator.netlify.app/)

---

## 📝 Cheat Sheet

```css
/* Container */
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 100px auto;
  gap: 20px;
  
  /* Alignment */
  justify-items: center;
  align-items: center;
  justify-content: space-between;
  align-content: start;
}

/* Items */
.item {
  grid-column: 1 / 3;        /* or: span 2 */
  grid-row: 2 / 4;           /* or: span 2 */
  grid-area: header;         /* named area */
  
  /* Alignment */
  justify-self: end;
  align-self: start;
}

/* Responsive */
.responsive {
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}
```

---

**Happy Gridding! 🎉**
