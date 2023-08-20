# Shopee Clone Project

## Features

- Authentication module: Manage by JWT

  - Register
  - Login
  - Logout

- Product List Page

  - Pagination
  - Sort
  - Filter
  - Search Product

- Product Detail Page

  - Show detail information of Product
  - Slider, hover zoom effect
  - Show rich text, WYSIWYG HTML
  - Add to cart, buy now

- Cart

  - Manage Order: add, edit, delete products
  - Buy

- User's Profile

  - Update information
  - Upload Avatar
  - Change Password
  - Show order's status

## Technology

- UI / CSS Library: Tailwindcss + HeadlessUI
- State Management: React Query for async state, React Context for others
- Form Management: React Hook Form
- Router: React Router
- Build tool: Vite
- API: Rest API by Duthanhduoc
- Multilanguage with react.i18next
- SEO friendly with React Helmet
- Story book
- Unit Test

## Installing packages for Vite React TS project

### Installing dependencies

### ESLint and Prettier setup

> We will install a few packages as we are setting up from scratch, whereas Create React App already has some ESLint setup.

Below are the dependencies that we need to install:

- ESLint: main linter for checking errors.

- Prettier: main code formatter

- @typescript-eslint/eslint-plugin: ESLint plugin providing rules for TypeScript.

- @typescript-eslint/parser: Parser allowing ESLint to check TypeScript errors.

- eslint-config-prettier: ESLint config to disable ESLint rules that conflict with Prettier.

- eslint-plugin-import: Enables ESLint to understand import... syntax in the source code.

- eslint-plugin-jsx-a11y: Checks accessibility-related issues (website friendliness, e.g., for screen readers).

- eslint-plugin-react: ESLint rules for React.

- eslint-plugin-prettier: Incorporates additional Prettier rules into ESLint.

- prettier-plugin-tailwindcss: Organizes Tailwind CSS class sorting.

- eslint-plugin-react-hooks: ESLint for React hooks.

Run the command below:

```bash
yarn add eslint prettier @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-config-prettier eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react eslint-plugin-prettier prettier-plugin-tailwindcss eslint-plugin-react-hooks -D
```

Configuring ESLint

Create file `.eslintrc.cjs` in root folder

```js
/* eslint-disable @typescript-eslint/no-var-requires */
const path = require("path");

module.exports = {
  extends: [
    // We use the default rules from the plugins that we have installed.
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:react-hooks/recommended",
    "plugin:import/recommended",
    "plugin:import/typescript",
    "plugin:jsx-a11y/recommended",
    "plugin:@typescript-eslint/recommended",
    // Disable confict rules
    // Put this bellow to override above
    "eslint-config-prettier",
    "prettier",
  ],
  plugins: ["prettier"],
  settings: {
    react: {
      // eslint-plugin-react knows React Version
      version: "detect",
    },
    // Eslint handle import
    "import/resolver": {
      node: {
        paths: [path.resolve(__dirname, "")],
        extensions: [".js", ".jsx", ".ts", ".tsx"],
      },
    },
  },
  env: {
    node: true,
  },
  rules: {
    // Tắt rule yêu cầu import React trong file jsx
    // Disable require import rule in jsx file
    "react/react-in-jsx-scope": "off",
    // Cảnh báo khi thẻ <a target='_blank'> mà không có rel="noreferrer"
    // Warning when <a target='_blank'> without rel="noreferrer"
    "react/jsx-no-target-blank": "warn",
    // Add some rule prettier (copy from file .prettierrc)
    "prettier/prettier": [
      "warn",
      {
        arrowParens: "always",
        semi: false,
        trailingComma: "none",
        tabWidth: 2,
        endOfLine: "auto",
        useTabs: false,
        singleQuote: true,
        printWidth: 120,
        jsxSingleQuote: true,
      },
    ],
  },
};
```

Create file `.eslintignore`

```json
node_modules/
dist/
```

Create file `.prettierrc`

```json
{
  "arrowParens": "always",
  "semi": false,
  "trailingComma": "none",
  "tabWidth": 2,
  "endOfLine": "auto",
  "useTabs": false,
  "singleQuote": true,
  "printWidth": 120,
  "jsxSingleQuote": true
}
```

Create file `.prettierignore`

```json
node_modules/
dist/
```

Add new script `package.json`

```json
  "scripts": {
    ...
    "lint": "eslint --ext ts,tsx src/",
    "lint:fix": "eslint --fix --ext ts,tsx src/",
    "prettier": "prettier --check \"src/**/(*.tsx|*.ts|*.css|*.scss)\"",
    "prettier:fix": "prettier --write \"src/**/(*.tsx|*.ts|*.css|*.scss)\""
  },
```

### Install editorconfig

Create file `.editorconfig` in root folder

```EditorConfig
[*]
indent_size = 2
indent_style = space
```

### Configure tsconfig.json

Set `"target": "ES2015"` and `"baseUrl": "."` in `compilerOptions`

### Install tailwindcss

Install these packages [https://tailwindcss.com/docs/guides/vite](https://tailwindcss.com/docs/guides/vite)

```bash
yarn add -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

Configure file config

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

Add into file `src/index.css`

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Configure vite config

Install package `@types/node` to use node js in file ts without errors

```bash
yarn add -D @types/node
```

file `vite.config.ts`

```ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import path from "path";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  server: {
    port: 3000,
  },
  css: {
    devSourcemap: true,
  },
  resolve: {
    alias: {
      src: path.resolve(__dirname, "./src"),
    },
  },
});
```

### Install extension and setup VS Code

Recommend Extensions:

- ESLint

- Prettier - Code formatter

- Tailwindcss

- EditorConfig for VS Code

Configure VS Code

- Enable Format On Save
- Set Default Formatter is Prettier

## Note coding

Code remove special character:

```ts
export const removeSpecialCharacter = (str: string) =>
  // eslint-disable-next-line no-useless-escape
  str.replace(
    /!|@|%|\^|\*|\(|\)|\+|\=|\<|\>|\?|\/|,|\.|\:|\;|\'|\"|\&|\#|\[|\]|~|\$|_|`|-|{|}|\||\\/g,
    ""
  );
```

Fix Tailwindcss Extension doesn not suggest class:

Add this code into `settings.json` of VS Code:

```json
{
  //...
  "tailwindCSS.experimental.classRegex": ["[a-zA-Z]*class[a-zA-Z]*='([^']+)'"]
}
```
