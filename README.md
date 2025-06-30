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


7. **Why Use Flexbox?**

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

_(Notes for this day to be added)_