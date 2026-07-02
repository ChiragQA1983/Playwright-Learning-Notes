# 🎯 Playwright Actions - Focus & Blur

## 📌 Focus and Blur Actions

The `focus()` and `blur()` methods are used to control the focus state of an element.

- **focus()** → Places the cursor (keyboard focus) on an element.
- **blur()** → Removes the keyboard focus from the currently focused element.

These methods are useful for testing form validation, input events, accessibility, and UI behavior that depends on gaining or losing focus.

Playwright automatically waits for the element to become available before performing these actions.

---

# Focus Action

## 📌 What is `focus()`?

The `focus()` method places keyboard focus on an element without clicking it.

It is commonly used before typing, pressing keyboard shortcuts, or triggering focus-related events.

---

# Syntax

```javascript
await page.locator('locator').focus();
```

> ✅ **Recommended:** Use `locator.focus()` because it is reliable and supports Playwright's auto-waiting mechanism.

---

# Example 1: Focus an Input Field

```javascript
import { test } from '@playwright/test';

test('Focus Input Field', async ({ page }) => {

    await page.goto('https://example.com');

    await page.locator('#username').focus();

});
```

---

# Example 2: Focus and Type

```javascript
await page.locator('#username').focus();

await page.keyboard.type('Admin');
```

---

# Example 3: Focus Using Different Locators

### By ID

```javascript
await page.locator('#email').focus();
```

### By Label

```javascript
await page.getByLabel('Email').focus();
```

### By Placeholder

```javascript
await page.getByPlaceholder('Enter Email').focus();
```

### By Role

```javascript
await page.getByRole('textbox').focus();
```

---

# Verify Focus

```javascript
await page.locator('#username').focus();

await expect(page.locator('#username')).toBeFocused();
```

---

# Blur Action

## 📌 What is `blur()`?

The `blur()` method removes keyboard focus from the currently focused element.

It is commonly used to trigger validation messages, save events, formatting logic, or `onBlur` event handlers.

---

# Syntax

```javascript
await page.locator('locator').blur();
```

---

# Example 1: Blur an Input Field

```javascript
await page.locator('#username').focus();

await page.locator('#username').blur();
```

---

# Example 2: Trigger Validation on Blur

```javascript
await page.locator('#email').fill('invalid-email');

await page.locator('#email').blur();

await expect(
    page.locator('.error-message')
).toBeVisible();
```

---

# Example 3: Blur Using Different Locators

### By ID

```javascript
await page.locator('#password').blur();
```

### By Label

```javascript
await page.getByLabel('Password').blur();
```

### By Placeholder

```javascript
await page.getByPlaceholder('Enter Password').blur();
```

### By Role

```javascript
await page.getByRole('textbox').blur();
```

---

# Difference Between Focus and Click

| Feature | `focus()` | `click()` |
|----------|-----------|-----------|
| Gives keyboard focus | ✅ Yes | ✅ Yes |
| Performs mouse click | ❌ No | ✅ Yes |
| Triggers click events | ❌ No | ✅ Yes |
| Best for keyboard testing | ✅ Yes | ❌ No |

---

# Difference Between Focus and Blur

| Method | Purpose |
|---------|---------|
| `focus()` | Places focus on an element |
| `blur()` | Removes focus from an element |

---

# Real-Time Use Cases

### Login Form

```javascript
await page.locator('#username').focus();

await page.keyboard.type('Admin');
```

---

### Validate Required Field

```javascript
await page.locator('#email').focus();

await page.locator('#email').blur();

await expect(
    page.locator('.required-error')
).toBeVisible();
```

---

### Trigger Auto Save

```javascript
await page.locator('#comments').fill('Updated Notes');

await page.locator('#comments').blur();
```

---

# Best Practices

✅ Use `focus()` when testing keyboard interactions.

✅ Use `blur()` to trigger validation or save events.

✅ Verify focus using `toBeFocused()`.

✅ Use assertions after blur to validate expected UI behavior.

✅ Avoid unnecessary `waitForTimeout()` before using focus or blur.

---

# Common Interview Questions

### Q1. What is the purpose of `focus()`?

**Answer:**

The `focus()` method places keyboard focus on an element without performing a mouse click.

---

### Q2. What is the purpose of `blur()`?

**Answer:**

The `blur()` method removes keyboard focus from an element and triggers blur-related events such as validation.

---

### Q3. What is the difference between `focus()` and `click()`?

**Answer:**

- `focus()` only places keyboard focus on an element.
- `click()` performs a mouse click, which usually also gives focus to the element.

---

### Q4. How do you verify that an element has focus?

**Answer:**

```javascript
await expect(
    page.locator('#username')
).toBeFocused();
```

---

### Q5. When is `blur()` commonly used?

**Answer:**

- Form validation
- Auto-save functionality
- Formatting inputs
- Triggering `onBlur` events
- Accessibility testing

---

# Summary

| Method | Purpose |
|--------|---------|
| `focus()` | Places keyboard focus on an element |
| `blur()` | Removes focus from an element |
| `toBeFocused()` | Verifies that an element has focus |
| `keyboard.type()` | Types into the focused element |

---

# Key Points

- `focus()` gives keyboard focus to an element without clicking it.
- `blur()` removes focus and triggers blur-related events.
- These methods are useful for testing form validation, accessibility, and keyboard interactions.
- Use `toBeFocused()` to verify the focused state.
- Combine `focus()`, `blur()`, and assertions to validate application behavior.
