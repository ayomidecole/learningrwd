Responsive Web Design
======================

I am using this space to document the code and the learnings from the Book
[Responsive Web Design](http://rwd.education) by Ben Frain

# Learnings


## 06/29/2025

1. Learnt about how the HTML  dialog box and how it works

```
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