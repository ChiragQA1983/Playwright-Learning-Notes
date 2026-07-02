# 🧹 Playwright Actions - Clear

## 📌 Clear Action

Playwright does not provide a dedicated `clear()` method like some automation frameworks. Instead, you can clear the contents of an input field by using the `fill('')` method, which replaces the existing value with an empty string.

This is the recommended and simplest way to clear text from input fields and textareas.

---

# Syntax

```javascript
await page.locator('locator').fill('');
```

or

```javascript
await page.fill('locator', '');
```

> ✅ **Recommended:** Use `locator().fill('')` because it is more reliable, reusable, and supports Playwright's auto-waiting mechanism.

---

# Example 1: Clear a Text Field

```javascript
import { test } from '@playwright/test';

test('Clear Username Field', async ({ page }) => {

    await page.goto('https://example.com/login');

    await page.locator('#username').fill('');

});
```

---

# Example 2: Clear Multiple Fields

```javascript
await page.locator('#username').fill('');

await page.locator('#password').fill('');

await page.locator('#email').fill('');
```

---

# Example 3: Clear Using Different Locators

### By ID

```javascript
await page.locator('#username').fill('');
```

### By Placeholder

```javascript
await page.getByPlaceholder('Enter Username').fill('');
```

### By Label

```javascript
await page.getByLabel('Username').fill('');
```

### By Role

```javascript
await page.getByRole('textbox').fill('');
```

### By CSS Selector

```javascript
await page.locator('input[name="username"]').fill('');
```

---

# Clear a Textarea

```javascript
await page.locator('#comments').fill('');
```

---

# Replace Existing Text

You can clear the existing value and immediately enter a new value using `fill()`.

```javascript
await page.locator('#username').fill('Admin');
```

This automatically removes the old value before entering the new one.

---

# Verify the Field is Empty

```javascript
await page.locator('#username').fill('');

await expect(page.locator('#username'))
    .toHaveValue('');
```

---

# Alternative Method: Select All + Delete

In some applications, especially those with custom input controls, you may need to simulate keyboard actions.

### Windows/Linux

```javascript
await page.locator('#username').click();

await page.keyboard.press('Control+A');

await page.keyboard.press('Delete');
```

### macOS

```javascript
await page.locator('#username').click();

await page.keyboard.press('Meta+A');

await page.keyboard.press('Delete');
```

> ⚠️ Use this approach only if `fill('')` does not work as expected.

---

# Difference Between `fill('')` and Keyboard Clear

| Feature | fill('') | Ctrl + A + Delete |
|----------|----------|-------------------|
| Clears text | ✅ Yes | ✅ Yes |
| Faster | ✅ Yes | ❌ No |
| Simulates user actions | ❌ No | ✅ Yes |
| Recommended | ✅ Yes | ⚠️ Only when required |

---

# Best Practices

✅ Use `fill('')` to clear input fields.

✅ Prefer `locator.fill('')` over `page.fill()`.

✅ Use keyboard shortcuts only for custom controls that do not respond to `fill('')`.

✅ Verify the field is empty using assertions when required.

✅ Avoid using `waitForTimeout()` before clearing fields.

---

# Common Interview Questions

### Q1. Does Playwright have a `clear()` method?

**Answer:**

No. Playwright does not provide a dedicated `clear()` method. The recommended way to clear a field is:

```javascript
await locator.fill('');
```

---

### Q2. How do you clear an input field?

**Answer:**

```javascript
await page.locator('#username').fill('');
```

---

### Q3. When should you use keyboard shortcuts to clear a field?

**Answer:**

Use `Control + A` (or `Meta + A` on macOS) followed by `Delete` when working with custom input components that do not respond correctly to `fill('')`.

---

### Q4. Can `fill('')` clear a textarea?

**Answer:**

Yes. It works for both input fields and textareas.

---

### Q5. Which approach is recommended?

**Answer:**

`locator.fill('')` is the recommended and most reliable approach because it automatically waits for the element to become editable.

---

# Summary

| Method | Purpose |
|--------|---------|
| `fill('')` | Clears an input field or textarea |
| `fill('New Value')` | Replaces the existing value |
| `keyboard.press('Control+A')` | Selects all text |
| `keyboard.press('Delete')` | Deletes selected text |
| `toHaveValue('')` | Verifies the field is empty |

---

# Key Points

- Playwright does **not** provide a dedicated `clear()` method.
- Use `fill('')` to clear input fields and textareas.
- `fill('')` is faster and more reliable than simulating keyboard shortcuts.
- Keyboard actions (`Ctrl + A` + `Delete`) are useful for custom input controls.
- Prefer `locator.fill('')` for better readability and maintainability.
