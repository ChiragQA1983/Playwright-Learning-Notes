# ☐ Playwright Actions - Uncheck

## 📌 Uncheck Action

The `uncheck()` method is used to **deselect a checkbox**. If the checkbox is already unchecked, Playwright does nothing. This makes the method safe to use without checking the checkbox state beforehand.

The `uncheck()` method automatically waits for the checkbox to become visible, enabled, and actionable before removing the check.

---

# Syntax

```javascript
await page.locator('locator').uncheck();
```

or

```javascript
await page.uncheck('locator');
```

> ✅ **Recommended:** Use `locator().uncheck()` because it is more reliable, reusable, and supports Playwright's auto-waiting mechanism.

---

# Example 1: Uncheck a Checkbox

```javascript
import { test } from '@playwright/test';

test('Uncheck Checkbox', async ({ page }) => {

    await page.goto('https://example.com');

    await page.locator('#rememberMe').uncheck();

});
```

---

# Example 2: Uncheck Using Different Locators

### By ID

```javascript
await page.locator('#agree').uncheck();
```

### By Label

```javascript
await page.getByLabel('Accept Terms').uncheck();
```

### By Role

```javascript
await page.getByRole('checkbox', {
    name: 'Remember Me'
}).uncheck();
```

### By CSS Selector

```javascript
await page.locator('input[type="checkbox"]').uncheck();
```

---

# Example 3: Uncheck Multiple Checkboxes

```javascript
await page.locator('#newsletter').uncheck();

await page.locator('#offers').uncheck();

await page.locator('#updates').uncheck();
```

---

# Verify Checkbox is Unchecked

```javascript
await page.locator('#rememberMe').uncheck();

await expect(
    page.locator('#rememberMe')
).not.toBeChecked();
```

---

# Uncheck Only If Checked

Although `uncheck()` automatically handles this, you can verify the state if needed.

```javascript
const checkbox = page.locator('#rememberMe');

if (await checkbox.isChecked()) {

    await checkbox.uncheck();

}
```

---

# Uncheck with Force Option

If Playwright determines that the checkbox is not interactable, you can force the action.

```javascript
await page.locator('#rememberMe').uncheck({
    force: true
});
```

> ⚠️ Use `force: true` only when absolutely necessary.

---

# Wait Before Unchecking

Playwright automatically waits until the checkbox is:

- Visible
- Enabled
- Stable
- Ready for interaction

```javascript
await page.locator('#rememberMe').uncheck();
```

No explicit wait is required in most cases.

---

# Difference Between `uncheck()` and `click()`

| Feature | uncheck() | click() |
|----------|-----------|----------|
| Deselects a checkbox | ✅ Yes | ✅ Yes |
| Works only with checkboxes | ✅ Yes | ❌ No |
| Avoids unnecessary clicks | ✅ Yes | ❌ No |
| Automatically verifies unchecked state | ✅ Yes | ❌ No |
| Recommended for checkboxes | ✅ Yes | ❌ No |

---

# Difference Between `check()` and `uncheck()`

| Method | Purpose |
|---------|---------|
| `check()` | Selects a checkbox |
| `uncheck()` | Deselects a checkbox |

---

# Best Practices

✅ Use `uncheck()` instead of `click()` to deselect checkboxes.

✅ Prefer `locator.uncheck()` over `page.uncheck()`.

✅ Use `getByRole()` or `getByLabel()` for better readability and accessibility.

✅ Verify the checkbox state using `.not.toBeChecked()`.

✅ Avoid using `force: true` unless absolutely required.

---

# Common Interview Questions

### Q1. What is the purpose of `uncheck()`?

**Answer:**

The `uncheck()` method deselects a checkbox. If the checkbox is already unchecked, Playwright performs no action.

---

### Q2. What happens if the checkbox is already unchecked?

**Answer:**

Playwright skips the action. It does not click the checkbox again.

---

### Q3. Why is `uncheck()` preferred over `click()`?

**Answer:**

`uncheck()` is specifically designed for checkboxes. It guarantees that the checkbox ends in an unchecked state without accidentally toggling it.

---

### Q4. How do you verify that a checkbox is unchecked?

**Answer:**

```javascript
await expect(
    page.locator('#rememberMe')
).not.toBeChecked();
```

---

### Q5. Does `uncheck()` automatically wait?

**Answer:**

Yes. Playwright automatically waits until the checkbox is visible, enabled, stable, and ready for interaction.

---

# Summary

| Method | Purpose |
|--------|---------|
| `uncheck()` | Deselects a checkbox |
| `isChecked()` | Returns the checkbox state |
| `not.toBeChecked()` | Verifies the checkbox is unchecked |
| `force: true` | Forces the uncheck action |
| `locator.uncheck()` | Recommended approach |

---

# Key Points

- `uncheck()` is used only for **checkboxes**.
- It does nothing if the checkbox is already unchecked.
- Playwright automatically waits before performing the action.
- Use `.not.toBeChecked()` to verify the checkbox is unchecked.
- Prefer `locator.uncheck()` over `page.uncheck()` for better readability, reliability, and maintainability.
