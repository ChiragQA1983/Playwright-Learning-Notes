# ☑️ Playwright Actions - Check

## 📌 Check Action

The `check()` method is used to **select a checkbox**. If the checkbox is already checked, Playwright does nothing. This makes the method safe to use without needing to verify the checkbox state first.

The `check()` method automatically waits for the checkbox to become visible, enabled, and actionable before selecting it.

---

# Syntax

```javascript
await page.locator('locator').check();
```

or

```javascript
await page.check('locator');
```

> ✅ **Recommended:** Use `locator().check()` because it is more reliable, reusable, and supports Playwright's auto-waiting mechanism.

---

# Example 1: Check a Checkbox

```javascript
import { test } from '@playwright/test';

test('Check Checkbox', async ({ page }) => {

    await page.goto('https://example.com');

    await page.locator('#rememberMe').check();

});
```

---

# Example 2: Check Using Different Locators

### By ID

```javascript
await page.locator('#agree').check();
```

### By Label

```javascript
await page.getByLabel('Accept Terms').check();
```

### By Role

```javascript
await page.getByRole('checkbox', {
    name: 'Remember Me'
}).check();
```

### By CSS Selector

```javascript
await page.locator('input[type="checkbox"]').check();
```

---

# Example 3: Check Multiple Checkboxes

```javascript
await page.locator('#newsletter').check();

await page.locator('#offers').check();

await page.locator('#updates').check();
```

---

# Verify Checkbox is Checked

```javascript
await page.locator('#rememberMe').check();

await expect(
    page.locator('#rememberMe')
).toBeChecked();
```

---

# Check Only If Not Already Checked

Although `check()` automatically handles this, you can verify the state if needed.

```javascript
const checkbox = page.locator('#rememberMe');

if (!(await checkbox.isChecked())) {

    await checkbox.check();

}
```

---

# Check with Force Option

If Playwright determines that the checkbox is not interactable, you can force the action.

```javascript
await page.locator('#rememberMe').check({
    force: true
});
```

> ⚠️ Use `force: true` only when necessary.

---

# Wait Before Checking

Playwright automatically waits until the checkbox is:

- Visible
- Enabled
- Stable
- Ready for interaction

```javascript
await page.locator('#rememberMe').check();
```

No explicit wait is required in most cases.

---

# Difference Between `check()` and `click()`

| Feature | check() | click() |
|----------|----------|----------|
| Selects a checkbox | ✅ Yes | ✅ Yes |
| Works only with checkboxes | ✅ Yes | ❌ No |
| Avoids unnecessary clicks | ✅ Yes | ❌ No |
| Automatically verifies checked state | ✅ Yes | ❌ No |
| Recommended for checkboxes | ✅ Yes | ❌ No |

---

# Best Practices

✅ Use `check()` instead of `click()` for checkboxes.

✅ Prefer `locator.check()` over `page.check()`.

✅ Use `getByRole()` or `getByLabel()` for better readability and accessibility.

✅ Verify the checkbox state using `toBeChecked()`.

✅ Avoid using `force: true` unless absolutely required.

---

# Common Interview Questions

### Q1. What is the purpose of `check()`?

**Answer:**

The `check()` method selects a checkbox. If the checkbox is already checked, Playwright does not perform any additional action.

---

### Q2. What happens if the checkbox is already checked?

**Answer:**

Playwright skips the action. It does not click the checkbox again.

---

### Q3. Why is `check()` preferred over `click()`?

**Answer:**

`check()` is specifically designed for checkboxes. It ensures the checkbox is selected without accidentally changing its state.

---

### Q4. How do you verify that a checkbox is selected?

**Answer:**

```javascript
await expect(
    page.locator('#rememberMe')
).toBeChecked();
```

---

### Q5. Does `check()` automatically wait?

**Answer:**

Yes. Playwright automatically waits until the checkbox is visible, enabled, stable, and ready for interaction.

---

# Summary

| Method | Purpose |
|--------|---------|
| `check()` | Selects a checkbox |
| `isChecked()` | Returns the checkbox state |
| `toBeChecked()` | Verifies the checkbox is selected |
| `force: true` | Forces the checkbox selection |
| `locator.check()` | Recommended approach |

---

# Key Points

- `check()` is used only for **checkboxes**.
- It does nothing if the checkbox is already checked.
- Playwright automatically waits before performing the action.
- Use `toBeChecked()` to verify the checkbox state.
- Prefer `locator.check()` over `page.check()` for better reliability and maintainability.
