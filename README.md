# Minimal Example of Vite (vanilla) + TS + TailwindCSS

This example follows the steps laid out in [Install Tailwind CSS with Vite
](https://tailwindcss.com/docs/guides/vite#react). The only exception is that Vite project was initialized as vanilla (no JS framework).

## Steps to reproduce:

Set up project and install libraries:

```
npm create vite@latest my-app -- --template vanilla-ts
cd my-app
npm install
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

Add the following to `src/style.css`

```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Edit `tailwind.config.js` to tell Tailwind which files to pick up styles from:

```js
/** @type {import('tailwindcss').Config} */
export default {
    content: [
        "./index.html", 
        "./src/**/*.{vue,js,ts,jsx,tsx}"
    ],
    theme: {
        extend: {},
    },
    plugins: [],
};
```

Your `src/main.ts` must import the styles file for it to be included in the build:

```ts
import "./style.css";
```

Finally, `npm run dev` or `npm run build` to see the result.

## Possible issues

### CSS file is not bundled in preview/build

Check if your `src/main.ts` imports the style file. Without importing it, the build will not have tailwind styles.

### Page flickers on reload / CSS takes a second to load

You can experience this if you are in preview mode. The mode loads styles with a delay and will show a popup if there is an issue in your styles/configuration. Check if the issue persists after building with `npm run build`.

### Cannot figure out how to extend Tailwind (e.g. add color presets)

Because the project template uses ES module (as opposed to CommonJS), it is not possible to use the `const colors = require('tailwindcss/colors');` as suggested by [Tailwind documentation](https://tailwindcss.com/docs/customizing-colors#using-the-default-colors). Instead, you can use the following code:

```js
import colors from "tailwindcss/colors";

/** @type {import('tailwindcss').Config} */
export default {
    content: [
        "./index.html",
        "./src/**/*.{vue,js,ts,jsx,tsx}"
    ],
    theme: {
        colors: {
            ...colors,
            primary: "rgb(255 0 0)",
            secondary: "#000",
        },
        extend: {},
    },
    plugins: [],
};
```
