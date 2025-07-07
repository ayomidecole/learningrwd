# Responsive Web Design

This document tracks my notes and code from the book [Responsive Web Design](http://rwd.education) by Ben Frain.

---

## Learnings

### 06/29/2025

1. **Dialog Element in HTML**

   The `<dialog>` element provides a native way to create dialog boxes in HTML. It's hidden by default and shown via JavaScript.

   ```html
   <body>
     <button id="launchDialog">Where is the dialog?</button>
     <p id="formResult"></p>
     <dialog id="dialogEle">
       <form method="dialog">
         <h1>How about this? A native Dialog.</h1>
         <p>So, only thing left to do is dismiss me.</p>
         <button value="Dismissed">Dismiss Dialog</button>
       </form>
     </dialog>
     <script>
       const dialogEle = document.getElementById('dialogEle');
       const launchBtn = document.getElementById('launchDialog');
       const formResult = document.getElementById('formResult');

       launchBtn.addEventListener("click", () => dialogEle.showModal());
       dialogEle.addEventListener('close', () => {
         formResult.textContent = dialogEle.returnValue;
       });
     </script>
   </body>
   ```

   - The `<dialog>` element is hidden until `showModal()` is called.
   - It can be closed by:
     - Clicking a `<button>` inside with `method="dialog"`.
     - Pressing Escape.
     - Calling `dialog.close()`.
   - The `returnValue` property is set to the `value` of the button that closed it.

2. **Meta Viewport Tag**

   The `<meta>` viewport tag controls how a page is scaled and displayed on mobile devices.

   ```html
   <meta 
     name="viewport"
     content="width=device-width, initial-scale=2.0, user-scalable=no"
   />
   ```

   - `width=device-width`: Page width matches device's screen.
   - `initial-scale=2.0`: Zooms in 2x by default.
   - `user-scalable=no`: Prevents zooming.

   The most common usage is:

   ```html
   <meta name="viewport" content="width=device-width, initial-scale=1.0" />
   ```

3. **Fluid Layouts**

   - Use percentage-based widths instead of fixed widths for flexible layouts.

4. **Media Queries**

   Media queries apply CSS rules based on device properties (like viewport width):

   ```css
   @media screen and (min-width: 550px) {
     body {
       background-color: yellow;
     }
   }
   ```

   Or, omitting `screen`:

   ```css
   @media (min-width: 550px) {
     body {
       background-color: yellow;
     }
   }
   ```

   The typical workflow is:
   - Write base styles for all devices.
   - Add media queries as the design "grows" to accommodate wider screens.

5. We can center an element within its parent element with:

```css
margin: 0 auto;
```

6. There are two important tools for responsive design:
    - Flexbox: For laying things out in one directions at a time
    - Grid: Laying things out in two directions at a time


7. **Flexbox**

   Flexbox is a CSS layout system that makes it easier to design flexible, responsive layouts. Here are some beginner-friendly reasons to use Flexbox:

   - **Easily Center Content Vertically and Horizontally**  
     With Flexbox, you can center items inside a container both up-and-down (vertically) and left-to-right (horizontally) with just a couple of CSS properties.

   - **Change the Order of Elements**  
     You can visually rearrange the order of items on the page without changing the HTML, just by using CSS.

   - **Automatic Spacing and Alignment**  
     Flexbox can automatically distribute space between items, align them to the start, end, or center, and make items expand to fill available space.

   - **Flexible Directions**  
     Items can be laid out in a row (left to right), row-reverse (right to left), column (top to bottom), or column-reverse (bottom to top).

   - **Responsive by Design**  
     Flexbox layouts adapt smoothly to different screen sizes and devices.

8. Flexbox has four key characteristics: direction, allignment, ordering and flexibility

9. In the code below from example 3 (`ch04/example3.html` and `ch04/example3.css`):

```css
.CenterMe {
    display: flex;
    align-items: center;
    justify-content: center;
}
```

- `display: flex;`  
  This turns the element into a flex container. All direct children of this element become flex items, which allows you to use powerful alignment and spacing features.

- `align-items: center;`  
  This vertically centers the flex items along the container's cross axis (which is up and down by default). It makes the children sit in the vertical middle of the container.

- `justify-content: center;`  
  This horizontally centers the flex items along the container's main axis (which is left to right by default). It moves the children into the horizontal center of the container.

Together, these three lines make it easy to perfectly center content (both vertically and horizontally) inside a container.

---

### 06/30/2025


1. Here’s a simple way to style a navigation bar using Flexbox:

```css
.container {
    background-color: indigo;
    font-family: "Oswald", sans-serif;
    font-size: 1rem;
    min-height: 2.75rem;
    display: flex;              /* Use Flexbox for layout */
    align-items: center;        /* Vertically center items */
    padding: 0 1rem;
}

/* Style for all navigation links */
.item,
.last-item {
    color: #ebebeb;
    text-decoration: none;
}

/* Space out the links except for the last one */
.item {
    margin-right: 1rem;
}

/* Push the last link ("Contact Us") to the far right */
.last-item {
    margin-left: auto;
}
```

![Navigation Bar](./Screenshot%202025-06-30%20at%206.33.44 PM.png)

**How does this work?**

- `.container` uses `display: flex;` to arrange its child elements (the navigation links) in a row.
- `align-items: center;` centers the links vertically inside the bar.
- `.item` uses `margin-right` to add space to the right of each link, separating them from the next link.
- `.last-item` uses `margin-left: auto;` which tells the browser to push it as far to the right as possible. This is a common Flexbox trick to separate one item from the rest—great for things like a “Contact Us” link in a navigation bar!

2. **Reverse the Order of Navigation Links**

To display the navigation links in reverse order (right-to-left), add this CSS to the `.container`:

```css
.container {
    flex-direction: row-reverse;
}
```

To push the "Contact Us" link to the far left in this reversed layout, update its style:

```css
.last-item {
    margin-right: auto;
}
```

![Reversed Nav Bar](./Screenshot%202025-06-30%20at%206.51.01 PM.png)

---

3. **Stack the Navbar Vertically**

To arrange the navigation links in a column (top-to-bottom), modify the `.container` like this:

```css
.container {
    flex-direction: column;
    align-items: center;
}
```

![Stacked Nav Bar](./Screenshot%202025-06-30%20at%206.54.52 PM.png)

---

### 07/01/2025

1. **Flexbox Alignment Properties**

Understanding Flexbox alignment starts with knowing the two axes:

- **Main Axis**
- **Cross Axis**

Which axis is which depends on the value of the `flex-direction` property:

- **`flex-direction: row`** (the default):  
  - Main axis: **horizontal** (left to right)
  - Cross axis: **vertical** (top to bottom)
- **`flex-direction: column`**:  
  - Main axis: **vertical** (top to bottom)
  - Cross axis: **horizontal** (left to right)

> **Note:**  
> - `justify-content` aligns items along the **main axis**.
> - `align-items` aligns items along the **cross axis**.
> - `align-content` aligns the entire flex lines (when wrapping) along the cross axis.

2. **Cross-Axis Alignment Values in Flexbox: `align-items` or `align-self`**

- `flex-start`: Align items to the start of the cross axis.
- `flex-end`: Align items to the end of the cross axis.
- `center`: Center items along the cross axis.
- `baseline`: Align items so their text baselines line up.
- `stretch`: Stretch items to fill the container (default).

3. **Main-Axis Alignment Values in Flexbox: `justify-content`**

- `flex-start`: Items are packed toward the start of the main axis (default).
- `flex-end`: Items are packed toward the end of the main axis.
- `center`: Items are centered along the main axis.
- `space-between`: Items are evenly distributed; first item at the start, last at the end.
- `space-around`: Items are evenly distributed with equal space around them.
- `space-evenly`: Items are distributed so the spacing between any two items (and the edges) is equal.

4. **Flexbox Shorthand: `flex`**

You can use the `flex` property as a shorthand to set how a flex item grows, shrinks, and what its initial size should be:

```css
.item {
  flex: 1 1 100px;
}
```

This means:

- `flex-grow: 1;` &nbsp;→ The item can grow to fill available space.
- `flex-shrink: 1;` &nbsp;→ The item can shrink if needed.
- `flex-basis: 100px;` &nbsp;→ The item starts at 100px wide (or tall, depending on direction).

So, each `.item` will start at 100px, but will stretch or shrink as needed to fit the container.

---

Another example:

```css
.item {
  flex: 0 0 33.33%;
}
```

This means:

- `flex-grow: 0;` &nbsp;→ The item will not grow to fill extra space.
- `flex-shrink: 0;` &nbsp;→ The item will not shrink smaller than its basis.
- `flex-basis: 33.33%;` &nbsp;→ The item will always be 33.33% of the container's width (or height, depending on direction).

So, each `.item` will take up exactly one third of the container and won’t stretch or shrink.

---

### 07/05/2025

1. **Grid**

   CSS Grid is a two-dimensional layout system, unlike Flexbox which handles only one dimension at a time. With Flexbox, you lay out items in either a row or a column. Grid allows you to lay out items in both rows and columns simultaneously.

2. **Basic Grid Syntax**

   When using Grid, you specify:
   - How many rows and columns the grid should have
   - How those rows and columns are sized
   - Where each grid item is placed
   - How the grid adapts when its size changes or when more items are added

3. **Setting Up a Grid Layout**

   To create a basic 2x2 grid, use the following CSS:

   ```css
   .my-first-grid {
       display: grid;
       grid-gap: 10px;
       grid-template-rows: 200px 200px;
       grid-template-columns: 200px 200px;
       background-color: #e4e4e4;
   }
   .grid-item-1 {
       grid-row: 1;
       grid-column: 1;
   }
   .grid-item-2 {
       grid-row: 2;
       grid-column: 2;
   }
   .grid-item-3 {
       grid-row: 1;
       grid-column: 2;
   }
   .grid-item-4 {
       grid-row: 2;
       grid-column: 1;
   }
   [class^='grid-item'] {
       outline: 3px dashed #f90;
       font-size: 30px;
       color: #3333;
       padding: 50% 50%;
   }
   ```
   - `.my-first-grid`: Turns the container into a 2x2 grid, adds gaps between cells, and sets a background color.
   - `.grid-item-*`: Places each item into a specific row and column within the grid using `grid-row` and `grid-column`.
   - `[class^='grid-item']`: Adds a dashed outline, increases the font size, applies semi-transparent text color, and centers the content with padding.

   ![My First Grid Example](./Screenshot%202025-07-05%20at%205.23.23 PM.png)

4. **Grid Alignment Properties**

   You can still use alignment properties from Flexbox in Grid:

   ```css
   .my-first-grid {
       display: grid;
       grid-gap: 10px;
       grid-template-rows: 200px 200px;
       grid-template-columns: 200px 200px;
       background-color: #e4e4e4;
       /* You can use alignment properties similar to Flexbox: */
       align-items: center;    /* Vertically center grid items within their cells */
       justify-items: center;  /* Horizontally center grid items within their cells */
       /* Or, to align the entire grid inside its parent: */
       /* justify-content: center; */
       /* align-content: center; */
   }
   ```

   ![Centered & Aligned Grid Example](./Screenshot%202025-07-05%20at%205.22.18 PM.png)

5. **Using `inline-grid` and Centering Content**

   By default, when you use `display: grid`, the grid container stretches to fill the entire width of its parent—even if your content doesn't need that much space. Sometimes, you want the grid to only be as wide as its content and sit nicely centered on the page.

   To do this, use `display: inline-grid` on the grid container. This makes the grid shrink-wrap its content. To center the items inside each grid cell, you can also use grid or flexbox alignment properties on the grid items.

   Here’s how you can do it:

   ```css
   .my-first-grid {
       display: inline-grid;              /* Grid only as wide as needed */
       grid-gap: 10px;
       grid-template-rows: 200px 200px;
       grid-template-columns: 200px 200px;
       background-color: #e4e4e4;
   }

   .grid-item-1 {
       grid-row: 1;
       grid-column: 1;
   }
   .grid-item-2 {
       grid-row: 2;
       grid-column: 2;
   }
   .grid-item-3 {
       grid-row: 1;
       grid-column: 2;
   }
   .grid-item-4 {
       grid-row: 2;
       grid-column: 1;
   }

   [class^='grid-item'] {
       display: grid;                  /* Makes each item a grid container */
       align-items: center;            /* Vertically center content */
       justify-content: center;        /* Horizontally center content */
       outline: 3px dashed #f90;
       font-size: 30px;
       color: black;
   }
   ```

   - `.my-first-grid` uses `inline-grid` so the grid container only takes up as much horizontal space as its content, instead of stretching to fill the whole page.
   - Each `.grid-item-*` is placed into a specific spot in the grid.
   - `[class^='grid-item']` turns each item into a grid container and centers its content both vertically and horizontally.

   ![Inline Grid Centered Example](./Screenshot%202025-07-05%20at%205.36.44 PM.png)

6. **Explicit and Implicit Grid**

   - **Explicit grid:** The grid you define directly with `grid-template-rows` and `grid-template-columns`.
   - **Implicit grid:** When you add more items than your explicit grid allows, CSS Grid automatically creates extra rows or columns to fit them—this is called the implicit grid.

   For example, if you have a 2x2 grid and add a fifth item like `<div class="grid-item-5">5</div>`, Grid creates an extra row for it:

   ![Grid with 5 Items (Implicit Row)](./Screenshot%202025-07-05%20at%207.10.50 PM.png)

   You can control the size of these implicitly created tracks using the `grid-auto-rows` and `grid-auto-columns` properties:
   ```css
   .my-first-grid {
       grid-auto-rows: 200px;
       grid-auto-columns: 200px;
   }
   ```
   - `grid-auto-rows: 200px;`  
     This sets the height of any new (implicit) rows the grid creates to 200 pixels each. If you add extra items that don't fit in the defined rows, the grid will make more rows, each 200px tall.

   - `grid-auto-columns: 200px;`  
     This sets the width of any new (implicit) columns the grid creates to 200 pixels each. If you have more items than defined columns, the grid will add extra columns, each 200px wide.

   ![Grid auto rows and columns example](./Screenshot%202025-07-05%20at%207.16.17 PM.png)

   Without any extra CSS, when we add more items to the grid, they are automatically placed into new rows or columns as needed.

7. You can also set *intermittent patterns* for implicit grid tracks.

   ```css
   .my-first-grid {
       display: inline-grid;
       grid-gap: 10px;
       grid-template-rows: 200px 200px;
       grid-template-columns: 200px 200px;
       grid-auto-rows: 100px 150px;      /* Alternates: first implicit row 100px, next 150px, then repeats */
       grid-auto-columns: 100px 150px;   /* Alternates: first implicit col 100px, next 150px, then repeats */
       background-color: #e4e4e4;
   }
   ```

   ![Grid with Intermittent Implicit Track Sizes](./Screenshot%202025-07-05%20at%207.42.19 PM.png)

8. **`grid-auto-flow`**

   The `grid-auto-flow` property controls how implicitly added items are placed in the grid—whether new items fill rows first (default), or columns first.

   - `grid-auto-flow: row;` (default): Extra items fill into new rows.
   - `grid-auto-flow: column;`: Extra items fill into new columns instead.

   For example, setting `grid-auto-flow: column` makes the grid add extra columns for new items, so the items flow horizontally across the page:

   ```css
   .my-first-grid {
       display: grid;
       grid-template-rows: 200px 200px;
       grid-template-columns: 200px 200px;
       grid-auto-flow: column;
       grid-gap: 10px;
       background-color: #e4e4e4;
   }
   ```

   ![Grid Auto Flow Column Example](./Screenshot%202025-07-05%20at%208.00.25 PM.png)

  ---

### 07/06/2025

1. **Placing and Sizing Grid Layout Items**

   Here are some beginner-friendly explanations for key CSS Grid properties:

   - **`gap`**:  
     The `gap` property adds space between grid rows and columns (like gutters).  
     - If you use one value, both rows and columns get the same space:  
       `gap: 20px;` (20px between all rows and columns)
     - If you use two values, the first is for rows and the second is for columns:  
       `gap: 10px 30px;` (10px between rows, 30px between columns)

   - **`repeat()`**:  
     The `repeat()` function helps you easily create grids with repeating patterns.  
     Example:  
     `grid-template-columns: repeat(4, 1fr);`  
     This means "make 4 columns, each 1 fraction of the available space wide."  
     The first number is how many times to repeat, the second is what to repeat (like a size).

   - **`fr` units**:  
     The `fr` unit stands for "fraction of available space".  
     - If you have `grid-template-columns: 2fr 1fr;`  
       The first column gets twice as much space as the second.
     - `fr` is a powerful way to make flexible layouts without hardcoding pixel values.

2. **Placing Items in a Grid**

   You can control where each grid item appears by specifying which grid lines it should start and end at. This is done with the `grid-column` and `grid-row` properties.

   - **Using `grid-column` and `grid-row`:**

     ```css
     .grid-item3 {
         grid-column: 2 / -1;
     }
     ```

     - `grid-column: 2 / -1;`  
       This means the item will start at the 2nd vertical grid line and stretch to the last grid line (`-1` is always the last line).  
       So, it spans from column 2 all the way to the end of the grid.

     ```css
     .grid-item4 {
         grid-row: 4 / 7;
     }
     ```

     - `grid-row: 4 / 7;`  
       This means the item will start at the 4th horizontal grid line and end at the 7th, spanning three rows in total.

   - The syntax for both properties is:  
     `property: start-line / end-line;`  
     The **start line** is where the item begins, the **end line** is where it stops (not inclusive).

3. **Using `span` to Stretch Across Tracks**

   Instead of specifying an exact end line, you can tell the item to span a certain number of rows or columns from the starting line:

   ```css
   .grid-item17 {
       grid-row: 6 / span 2;
       grid-column: 2 / 3;
   }
   ```

   - `grid-row: 6 / span 2;`  
     This starts the item at row line 6 and makes it span 2 rows downward.
   - `grid-column: 2 / 3;`  
     This puts the item in the 2nd column only.

   **Summary:**  
   - Use `grid-column` and `grid-row` to place and size grid items by lines.
   - Use `span` to make an item stretch across multiple rows or columns from its starting line.

### 07/07/2025

1. **Named Grid Lines**

   CSS Grid lets you assign names to grid lines by putting names in square brackets (`[]`) within your `grid-template-columns` or `grid-template-rows`. This makes layouts easier to read and maintain!

   For example:
   - The first vertical line is named `left-start`
   - The second line is named both `left-end` and `center-start`
   - The third line is named both `center-end` and `right-start`
   - The last line is named `right-end`

   ```css
   .my-first-grid {
       display: inline-grid;
       gap: 10px;
       grid-template-columns:
           [left-start] 200px
           [left-end center-start] 200px
           [center-end right-start] 200px
           [right-end];
       grid-template-rows:
           [top-start] 200px
           [top-end middle-start] 200px
           [middle-end bottom-start] 200px
           [bottom-end];
       background-color: #e4e4e4;
   }
   ```

   - You can now position items using these names instead of numbers.  
     For example, to stretch an item from `left-start` to `center-end`:  
     `grid-column: left-start / center-end;`

2. **Using Named Grid Areas for Easy Placement**

   CSS Grid provides a shortcut for placing items if your grid line names end with `-start` and `-end`. When you do this, Grid automatically creates *named grid areas* for you.

   With named areas, you can position items using the `grid-area` property. The syntax is:

   ```
   grid-area: row-start / column-start;
   ```

   Here’s an example using a grid with named lines:

   ```css
   .grid-item-1 {
       grid-area: middle / center;
   }

   .grid-item-2 {
       grid-area: bottom / right;
   }

   .grid-item-3 {
       grid-area: top / left;
   }
   ```

   - `grid-area: middle / center;`  
     This places the item at the intersection of the row named `middle` and the column named `center`.
   - `grid-area: bottom / right;`  
     This places the item at the row named `bottom` and column named `right`.
   - `grid-area: top / left;`  
     This places the item at the row named `top` and column named `left`.

   **Why is this useful?**  
   Instead of remembering grid line numbers, you can use meaningful names, making your CSS easier to read and maintain!

3. **`grid-template-areas`**

   The `grid-template-areas` property lets you visually describe your grid layout by naming each cell. Each quoted line creates a row, and within each line, you specify the area name for each cell (space-separated). For example:

   ```css
   .my-first-grid {
       display: grid;
       grid-template-areas:
           "one two three"
           "four five six"
           "seven eight nine";
       grid-template-columns: 100px 100px 100px;
       grid-template-rows: 100px 100px 100px;
       gap: 10px;
   }
   ```

   Now, you can assign each grid item to a named area using `grid-area`:

   ```css
   .grid-item-1 {
       grid-area: five;
   }
   .grid-item-2 {
       grid-area: nine;
   }
   .grid-item-3 {
       grid-area: one;
   }
   ```

   This approach makes your layout much more readable, since you’re using descriptive area names rather than line numbers.

4. **`auto-fit` and `auto-fill`**

  `auto-fit` and `auto-fill` are "repeat-to-fill" keywords used to automatically create as many columns as will fit in the container.

    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));

5. **The `minmax()` Function in CSS Grid**

The `minmax()` function is used in CSS Grid to set a minimum and maximum size for a track (a row or column). This is super useful when you want your grid cells to be flexible: big enough to fit the content, but never too small or too large.

For example, if you want each column to be at least 200px wide but grow to fill available space (up to 1 fraction of the container), you can write:

```css
.my-first-grid {
    display: grid;
    grid-template-columns: repeat(3, minmax(200px, 1fr));
    gap: 10px;
}
```

- `minmax(200px, 1fr)` means:  
  "This column should be no smaller than 200px, but can grow up to fill a share of the available space (1fr = one fraction)."

Why is this powerful?  
- It lets your layout adapt: columns won't shrink below a certain point, which keeps content readable, but will expand to fill the container as needed.
- It's often used together with `auto-fit` or `auto-fill` to make *responsive* grids that look good on any screen size.

Try combining it with the previous example:

```css
grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
```

Now, as the container gets wider or narrower, the grid will add or remove columns, and each column will always be at least 200px wide but stretch as needed!


6. **Anatomy of a CSS rule**
  ```css
    .selector {
      /* comment */
      property: value; /* declaratiom */
    }
  ```

7. **Pseudo-elements and Pseudo-classes**

   - **Pseudo-classes** let you style elements based on their state or position (like when you hover over a link, or target only the first child in a list).  
     Example: `a:hover { color: red; }` makes links turn red when you hover your mouse over them.

   - **Pseudo-elements** let you style specific parts of an element, such as the first letter or line, or add decorative content before/after an element.  
     Example: `p::first-line { font-weight: bold; }` makes just the first line of every paragraph bold.

   Both start with a colon (`:`), but pseudo-elements use two (`::`) in modern CSS.