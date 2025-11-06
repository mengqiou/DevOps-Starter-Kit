# 🧭 Runtime & Execution Knowledge

Understanding how **JavaScript (JS)** and **TypeScript (TS)** run is essential for any modern web or backend developer. This guide systematically untangles the common concepts and nuances between *interpreting, compiling, and executing* these two languages.

---

## 🟨 JavaScript: The Interpreted Core

### What JavaScript Is

* JavaScript is an **interpreted** language — it runs directly in a **runtime environment** (browser or Node.js) without a separate compile step.
* The browser or Node.js uses a **JS engine** (e.g. Chrome’s *V8*, Firefox’s *SpiderMonkey*) to interpret and execute code line by line.

### Common JS Runtimes

| Environment | Description                                           | Example Command                   |
| ----------- | ----------------------------------------------------- | --------------------------------- |
| **Browser** | Runs JS for frontend logic                            | `<script src="main.js"></script>` |
| **Node.js** | Runs JS outside the browser (backend, tools, scripts) | `node app.js`                     |

### Key Tools

* **Node.js** → The runtime that executes JS outside browsers.
* **npm (Node Package Manager)** → Installs and manages JS libraries.

  ```bash
  npm install express
  ```

### Summary

> JS does **not need compilation** — it’s run directly by the runtime. But modern projects often use build steps (like bundlers) for optimisation, not because JS itself requires compiling.

---

## 🟦 TypeScript: Superset That Compiles to JS

### What TypeScript Is

* TypeScript adds **static typing** and **compiler checks** on top of JavaScript.
* Browsers and Node.js **cannot** execute `.ts` files directly.
* TypeScript must first be **compiled (transpiled)** to plain JS.

### The TypeScript Compiler (tsc)

| Tool        | Purpose                                          | Example                |
| ----------- | ------------------------------------------------ | ---------------------- |
| **tsc**     | Compiles `.ts` → `.js`                           | `tsc index.ts`         |
| **ts-node** | Runs TS files directly (auto-compiles in memory) | `npx ts-node index.ts` |

Example workflow:

```bash
# Compile
npx tsc main.ts
# Run compiled JS
node main.js
```

### Why Compilation Matters

* TS helps catch **type errors** before runtime.
* During compilation, `tsc` converts newer syntax and type annotations into plain JS.
* The compiler obeys the project’s **tsconfig.json**, which defines target JS version, output folder, etc.

Example:

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "outDir": "dist",
    "strict": true
  }
}
```

---

## 🧩 JSX & TSX Files

### JSX

* A syntax extension used in **React** that allows HTML-like syntax in JS.

  ```jsx
  const App = () => <h1>Hello World</h1>;
  ```

### TSX

* TypeScript + JSX = `.tsx`
* Used when writing React components in TypeScript.
* Must be compiled using a build tool or TypeScript compiler with JSX support.

  ```tsx
  const App: React.FC = () => <h1>Welcome</h1>;
  ```

---

## ⚙️ The Toolchain Summary

| Concept            | JS                      | TS                               |
| ------------------ | ----------------------- | -------------------------------- |
| File Extension     | `.js`                   | `.ts`, `.tsx`                    |
| Execution          | Direct via Node/browser | Needs compilation first          |
| Core Tool          | Node.js                 | `tsc` (TypeScript compiler)      |
| Optional Runner    | –                       | `ts-node` (on-the-fly execution) |
| Common Build Tools | Vite, Webpack, Parcel   | Same + integrates with `tsc`     |
| Language Features  | Dynamic typing          | Static typing + JS features      |

---

## 🔄 Typical Lifecycle Comparison

| Step                     | JavaScript        | TypeScript                        |
| ------------------------ | ----------------- | --------------------------------- |
| 1️⃣ Write Code           | `main.js`         | `main.ts`                         |
| 2️⃣ Install Dependencies | `npm install`     | `npm install typescript`          |
| 3️⃣ Run                  | `node main.js`    | `npx tsc main.ts && node main.js` |
| 4️⃣ (Optional) Auto Run  | `nodemon main.js` | `ts-node-dev main.ts`             |

---

## 🧠 Key Takeaways

* **JavaScript runs directly**, no compile step required.
* **TypeScript compiles to JS** before execution.
* The **TypeScript compiler (`tsc`)** ensures type safety and converts TS → JS.
* **JSX/TSX** require build tools to convert component syntax to normal JS.
* **npm/npx** are package and execution helpers — they’re not compilers themselves.

---

> 🔍 In essence: **JavaScript is executed, TypeScript is compiled and then executed.**
