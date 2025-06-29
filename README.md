Responsive Web Design
======================

I am using this space to document the code and the learnings from the Book
[Responsive Web Design](http://rwd.education) by Ben Frain

# Learnings


## 06/29/2025

1. Learnt about how the HTML  dialog box and how it works

```html
<body>
    <button id="launchDialog">Where is the dialog?</button>
    <p id="formResult"></p>
    <dialog id="dialogEle">
        <form method="dialog">
            <h1>How about this? A native Dialog.</h1>
            <p>So, only thing left to do is dismiss me.</p>
            <button value="Disnmissed">Dismiss Dialog</button>
        </form>
    </dialog>
    <script>
        const dialogEle = document.getElementById('dialogEle');
        const launchBtn = document.getElementById('launchDialog');
        const formResult = document.getElementById('formResult');

        launchBtn.addEventListener("click", () => dialogEle.showModal());
        dialogEle.addEventListener('close', () => {
            formResult.textContent = dialogEle.returnValue;
        })
    </script>
</body>
```

The `<dialog>` element is hidden by default and requires JavaScript's `showModal()` method to become visible. It can be closed in several ways:
- Clicking a button with `formmethod="dialog"` inside the dialog
- Pressing the Escape key
- Programmatically with `dialog.close()`

The `returnValue` property is automatically set to the `value` of the button that closed the dialog, allowing you to determine which action was taken.

2. Delved deeper into media queries, which allow us to target specific CSS styles depending on device capabilities.

    ### `<meta>` viewport tag

    The `<meta>` viewport tag allows web pages to communicate to mobile browsers how the content should be scaled and rendered.

    ```html
    <meta 
        name="viewport"
        content="width=device-width, initial-scale=2.0, user-scalable=no"
    />
    ```

    In the meta tag above, which should be placed in the `<head>` section of the HTML document:

    - `name="viewport"` tells the browser to apply viewport settings.
    - `width=device-width` sets the page width to match the device's screen width.
    - `initial-scale=2.0` sets the initial zoom level to 2x.
    - `user-scalable=no` prevents the user from zooming in or out.

    These settings help ensure your website looks and behaves correctly on various devices.

    The most common configuration of the `<meta>` tag is:

    ```html
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    ```

3. For fluid layouts you should use percentages rather than fixed widths.

4. ### Media Queries

    This is the media query syntax:

    ```css
    @media screen and (min-width: 550px) {
        body{
            background-color: yellow;
        }
    }
    ```

    This basically means that at that width 550px and larger, apply the css styles below. You can also express media queries without the screen

    ```css
    @media (min-width: 550px) {
        body{
            background-color: yellow;
        }
    }
    ```

When working with Media Queries we usually start by writing the basic styles without media queries and work wider and wider adding media queries and changes wherever needed to affect the design as required.