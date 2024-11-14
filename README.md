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

```
/** @type {import('tailwindcss').Config} */
export default {
    content: [
        './index.html',
        './src/**/*.{vue,js,ts,jsx,tsx}',
    ],
    theme: {
        extend: {},
    },
    plugins: [],
}
```

Your `src/main.ts` must import the styles file for it to be included in the build:

```
import "./style.css";
```

Finally, `npm run dev` or `npm run build` to see the result.
