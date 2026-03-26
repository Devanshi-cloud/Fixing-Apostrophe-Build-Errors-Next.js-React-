## 🛠️ Fixing Apostrophe Issues in Next.js Builds

### 📌 Overview

During the build process, the application failed due to unescaped apostrophes in JSX/TSX files.
Common examples included:

* `We'll`
* `We'd`

While these look harmless, they can cause parsing or linting issues depending on the configuration.

---

### ⚠️ Why This Happens

JSX can misinterpret apostrophes (`'`) in certain contexts, especially when strict linting or HTML parsing rules are applied. This may lead to unexpected build failures.

---

### ✅ Solution

To ensure compatibility, apostrophes were replaced with HTML entities:

| Original | Fixed |
| -------- | ----- |
| We'll    | We'll |
| We'd     | We'd  |

---

### 🧰 Fix Script

The following Python script was used to safely update the file:

```python
#!/usr/bin/env python3

file_path = 'path/to/your/file.tsx'

with open(file_path, 'r', encoding='utf-8') as f:
    content = f.read()

will_count = content.count("We'll")
would_count = content.count("We'd")

new_content = content.replace("We'll", "We&apos;ll")
new_content = new_content.replace("We'd", "We&apos;d")

if new_content != content:
    with open(file_path, 'w', encoding='utf-8') as f:
        f.write(new_content)

    print("File updated successfully")
    print(f"Replaced {will_count} occurrence(s) of We'll")
    print(f"Replaced {would_count} occurrence(s) of We'd")
else:
    print("No changes needed")
```

---

### 🔍 Debugging Tips

* Check if problematic text exists:

  ```python
  print("We'll" in content)
  ```

* View surrounding context safely:

  ```python
  idx = content.find("We'll")
  if idx != -1:
      print(content[max(0, idx-10):idx+20])
  ```

---

### ⚡ Alternative (One-liner)

To apply the fix across the entire repository:

```bash
grep -rl "We'll" . | xargs sed -i '' "s/We'll/We\\&apos;ll/g"
grep -rl "We'd" . | xargs sed -i '' "s/We'd/We\\&apos;d/g"
```

---

### 🎯 Result

* ✅ Build errors resolved
* ✅ JSX parsing issues eliminated
* ✅ Consistent handling of apostrophes across the codebase

---

### 💡 Recommendation

To avoid similar issues in the future:

* Use HTML entities like `&apos;` in JSX text
* Or wrap strings in JavaScript expressions:

  ```jsx
  {"We'll contact you soon"}
  ```
