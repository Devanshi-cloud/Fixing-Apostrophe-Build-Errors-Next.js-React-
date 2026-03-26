# 🛠️ Fixing ESLint & Build Errors in Next.js (Guide)

This guide helps you fix common ESLint and build errors in a **Next.js + TypeScript** project. If your build is failing, follow the steps below to quickly clean and fix your codebase.

---

## 🚨 Common Errors You May See

* `Run autofix to sort these imports!`
* `react/no-unescaped-entities`
* `@typescript-eslint/no-unused-vars`
* `react-hooks/exhaustive-deps`
* Warnings about `<img>` usage

---

## ✅ Step-by-Step Fix

### 1️⃣ Auto-fix Formatting (Prettier)

Run:

```bash
npx prettier --write .
```

---

### 2️⃣ Auto-fix ESLint Issues

```bash
npx eslint . --fix
```

---

## 🔧 Manual Fixes (Important)

### 🔹 1. Fix Unescaped Characters

**Error:**

```jsx
<p>It's working</p>
```

**Fix:**

```jsx
<p>It&apos;s working</p>
```

---

### 🔹 2. Remove or Fix Unused Variables

**Error Example:**

```ts
const router = useRouter()
```

#### ✅ Option A: Remove (Recommended)

Delete unused variables if not needed.

#### ✅ Option B: Prefix with `_`

```ts
const _router = useRouter()
```

---

### 🔹 3. Fix React Hook Dependencies

**Error:**

```ts
useEffect(() => {
  console.log(data)
}, [])
```

**Fix:**

```ts
useEffect(() => {
  console.log(data)
}, [data])
```

---

### 🔹 4. Replace `<img>` (Optional but Recommended)

**Before:**

```jsx
<img src="/image.png" />
```

**After:**

```tsx
import Image from "next/image"

<Image src="/image.png" alt="image" width={500} height={300} />
```

---

## 🚀 Final Step: Build Again

```bash
npm run build
```

---

## ⚡ Best Practice (Recommended Scripts)

Add this to your `package.json`:

```json
"scripts": {
  "format": "prettier --write .",
  "lint:fix": "eslint . --fix"
}
```

Then run:

```bash
npm run format
npm run lint:fix
```

---

## 🤖 AI Auto-Fix Prompt (For Tools like Antigravity)

Use this prompt to automatically fix issues:

```
Fix all ESLint and build errors in my Next.js TypeScript project.

- Sort imports using simple-import-sort
- Replace unescaped characters like ' with &apos;
- Remove unused variables and imports
- Prefix unused variables with _ if needed
- Fix React Hook dependencies (useEffect, useCallback)
- Format code using Prettier
- Ensure npm run build passes without errors
- Keep code clean and production-ready
```

---

## 🎯 Goal

✔ No ESLint errors
✔ Clean, consistent code
✔ Successful `npm run build`

---

## 💡 Tip

If errors persist, fix them file-by-file starting with the ones that have the most issues (e.g., `CareerPage.tsx`).

---

Happy coding 🚀
