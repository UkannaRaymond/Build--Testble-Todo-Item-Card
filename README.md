# Todo Item Card

A self-contained, interactive task card component built with vanilla HTML, CSS, and JavaScript. No dependencies, no build step.

---

## How to Run Locally

### Option 1 — Clone the repo

```bash
git clone https://github.com/UkannaRaymond/Build--Testble-Todo-Item-Card.git
cd todo-item-card
```

Then open the file directly in your browser:

```
open todo-item-card.html        # macOS
start todo-item-card.html       # Windows
xdg-open todo-item-card.html    # Linux
```

Or serve it locally to avoid any file-protocol quirks:

```bash
npx serve .
# then visit http://localhost:3000
```

### Option 2 — Download manually

Download both files into the same directory:

- `todo-item-card.html`
- `todo-item-card.css`

Then open `todo-item-card.html` in any modern browser.

No npm install, no bundler, no framework.

---

## Features

| Interaction          | Behaviour                                                                                                                                                  |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Checkbox**         | Marks card as complete — fades the card, strikes through the title, flips the status badge to "Done"                                                       |
| **Edit**             | Swaps the title, description, and priority badge in-place with editable inputs; "Save" writes the values back                                              |
| **Delete**           | Confirms, then fades and shrinks the card out before removing it from the DOM                                                                              |
| **Due date & timer** | Calculated relative to a hardcoded offset (`now + ~3 days 5 hours`); refreshes every 45 seconds; colours shift to amber when due soon and red when overdue |
| **Dark mode**        | Automatic via `prefers-color-scheme: dark` — no toggle needed                                                                                              |

---

## Decisions Made

### Vanilla stack

The card is a single HTML file with an external stylesheet and an inline script. This keeps the component portable and dependency-free — useful as a prototype or a drop-in reference implementation before migrating into a component framework.

### CSS-only theming via `prefers-color-scheme`

Rather than a JavaScript toggle, dark mode is handled entirely in CSS. This means it respects the OS setting immediately on load with zero flash of the wrong theme, and requires no state management.

### `data-testid` attributes on every interactive element

Every meaningful element carries a `data-testid` attribute (e.g. `test-todo-complete-toggle`, `test-todo-edit-button`). These are targeting hooks for automated tests and are intentionally kept separate from styling classes so that tests don't break when styles are refactored.

### In-place DOM replacement for edit mode

When the user clicks "Edit", the title `<h2>`, description `<p>`, and priority `<span>` are individually replaced with form controls (`<input>`, `<textarea>`, `<select>`), and restored on "Save". This avoids maintaining a parallel hidden-fields layer and keeps the DOM minimal, but it does mean the elements are re-created on every edit cycle rather than toggling visibility.

### Relative due-date calculation

The due date is derived from `Date.now()` at page load rather than being pulled from a data source. This makes the demo self-contained and always shows a meaningful "due in N days" state without requiring a backend or localStorage.

👤 Author
Ukanna Raymond | Frontend | Backend |

This project is part of my portfolio, showcasing the frontend skill for a fullstack role. If you have any questions, feedback, or would like to collaborate, feel free to get in touch!
