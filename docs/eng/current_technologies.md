# Current Technologies for Styling and UI – ITA Wiki 🛠️

## I. Main lib

This project mainly uses **Tailwind CSS**:

```json
"tailwindcss": "^4.0.14",
"@tailwindcss/vite": "^4.0.14"
```
✅ Strength: Quick and easy responsive pages with utility classes.


---

## II. Global Styles

The project defines **general CSS variables** in :root (index.css) for consistent styling.



<details>
  <summary>📂 SOURCE CODE INDEX.CSS</summary>


```css
@import "tailwindcss";

:root {
  font-family: "Poppins", system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;
  height: 100%;
  color-scheme: light dark;

  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #213547;
  background-color: #ffffff;

  --color-primary: #b91879;
}


@theme {
  --color-primary: #b91879;
  --color-gray-foreground: #7e7e7e;
  --background-image-card: url("assets/bg-card.svg");
}

a {
  font-weight: 500;
  color: #7e7e7e;
  text-decoration: inherit;
}

a:hover {
  color: #b91879;
}

body {
  margin: 0;
  min-width: 320px;
  min-height: 100vh;
  background-color: #ebebeb;
}

.text-green-custom {
  color: rgb(39, 174, 96);
}

.fill-green-custom {
  fill: rgb(39, 174, 96);
  stroke: rgb(39, 174, 96);
}

/* @media (prefers-color-scheme: light) {
  :root {
    color: #213547;
    background-color: #ffffff;
  }

  a:hover {
    color: #747bff;
  }
} */

```
</details>

#### 👉 About `@theme`

In Tailwind CSS v4+, `@theme { … }` lets you define CSS variables centrally instead of using `tailwind.config.js`.  

It’s mainly useful if you plan to support multiple themes (e.g., light/dark), as it allows switching variable values easily.  

Some editors may show warnings (`Unknown at rule @theme`), but this doesn’t affect the app.  

For simplicity and compatibility, especially without multiple themes, it’s recommended to define variables in `:root`.  

#### 👉 About `var()`


⚠ Remember:
> You can use the variables defined in `:root` (or `@theme`) with the `var()` function. 


```css
 .my-button {
 background-color: var(--color-primary);
 } 
```

```html
<button class="my-button">Click</button>
```

---

## III. Sonner Toast Library

**Sonner**  is a lightweight React toast notification library (~34.5 KB minified, 9.3 KB gzipped) that supports multiple toast types, customizable positioning, smooth animations, and promise-based toasts. Install via npm install sonner, add <Toaster /> to your app, and trigger notifications with toast().

> In this project, Sonner is the only library used for rendering toasts. Modals are handled manually and are not managed by Sonner.

---

## IV. Inline CSS

In some parts of the project, inline CSS styles are used directly on elements, typically for quick adjustments or dynamic styling that isn’t handled via Tailwind classes or CSS variables.

---

## V. Icon Sources in the Project

The project uses icons from multiple sources, organized as follows:

- **Lucide React**
- **React Icons**
- **SVG**
  - **Direct SVG files in assets** (copied from external sources)
  - **Custom-made icons**
    - **Used inline**
    - **From our own library** (`/icons`)

---

## VI. Conditional Styling

Conditional styling in the project is done in two main ways:

1. **String concatenation** (Tailwind only):

```tsx
export const App = () => {
  const primary = true;

  return (
    <div className="flex gap-4">
      <button
        className={
          "px-4 py-2 rounded font-bold transition cursor-pointer " +
          (primary
            ? "bg-[#B91879] text-white border-none hover:opacity-90"
            : "bg-white text-[#282828] border-2 border-[#282828] hover:opacity-90")
        }
      >
        {primary ? "Primary" : "Secondary"}
      </button>
    </div>
  );
};

```


2. **Using `clsx` or `classNames`** :

 Simplifies conditional classes, especially when many conditions exist.

This approach helps keep Tailwind classes organized and readable, avoiding long concatenated strings.


* "classnames": "^2.5.1",
* "clsx": "^2.1.1"

```tsx

import clsx from "clsx";

const Button = ({ primary }: { primary: boolean }) => {
  return (
    <button
      className={clsx(
        "px-4 py-2 rounded font-bold transition cursor-pointer",
        primary ? "bg-[#B91879] text-white" : "bg-white text-[#282828] border-2 border-[#282828]"
      )}
    >
      {primary ? "Primary" : "Secondary"}
    </button>
  );
};


```












