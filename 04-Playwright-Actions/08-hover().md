# 🖱️ Playwright Actions - Hover

## 📌 Hover Action

The `hover()` method is used to move the mouse pointer over an element without clicking it. It is commonly used to trigger hover effects such as dropdown menus, tooltips, hidden buttons, and submenu navigation.

Playwright automatically waits for the element to become visible, stable, and ready before performing the hover action.

---

# Syntax

```javascript
await page.locator('locator').hover();
```

or

```javascript
await page.hover('locator');
```

> ✅ **Recommended:** Use `locator().hover()` because it is more reliable, reusable, and supports Playwright's auto-waiting mechanism.

---

# Example 1: Hover Over an Element

```javascript
import { test } from '@playwright/test';

test('Hover Over Menu', async ({ page }) => {

    await page.goto('https://example.com');

    await page.locator('#menu').hover();

});
```

---

# Example 2: Hover to Open a Dropdown Menu

```javascript
await page.locator('#productsMenu').hover();

await page.locator('#softwareOption').click();
```

---

# Example 3: Hover Using Different Locators

### By ID

```javascript
await page.locator('#profile').hover();
```

### By Text

```javascript
await page.getByText('Products').hover();
```

### By Role

```javascript
await page.getByRole('link', {
    name: 'Products'
}).hover();
```

### By CSS Selector

```javascript
await page.locator('.menu-item').hover();
```

---

# Example 4: Hover and Verify Tooltip

```javascript
await page.locator('#helpIcon').hover();

await expect(
    page.locator('.tooltip')
).toBeVisible();
```

---

# Example 5: Hover Before Clicking

Some applications display hidden buttons only after hovering.

```javascript
await page.locator('.product-card').hover();

await page.locator('.add-to-cart').click();
```

---

# Example 6: Hover Over Multiple Elements

```javascript
await page.locator('#menu1').hover();

await page.locator('#menu2').hover();

await page.locator('#menu3').hover();
```

---

# Hover with Force Option

If Playwright determines that the element is not interactable, you can force the hover action.

```javascript
await page.locator('#menu').hover({

    force: true

});
```

> ⚠️ Use `force: true` only when absolutely necessary.

---

# Wait Before Hovering

Playwright automatically waits until the element is:

- Visible
- Stable
- Ready for interaction

```javascript
await page.locator('#menu').hover();
```

No explicit wait is required in most cases.

---

# Difference Between `hover()` and `click()`

| Feature | hover() | click() |
|----------|----------|----------|
| Moves mouse pointer | ✅ Yes | ❌ No |
| Clicks the element | ❌ No | ✅ Yes |
| Opens hover menus | ✅ Yes | ❌ No |
| Displays tooltips | ✅ Yes | ❌ No |
| Triggers hover effects | ✅ Yes | ❌ No |

---

# Real-Time Use Cases

### Open Navigation Menu

```javascript
await page.locator('#products').hover();

await page.locator('text=Software').click();
```

---

### Display Tooltip

```javascript
await page.locator('#infoIcon').hover();

await expect(
    page.locator('.tooltip')
).toContainText('More Information');
```

---

### Show Hidden Action Button

```javascript
await page.locator('.employee-row').hover();

await page.getByRole('button', {
    name: 'Edit'
}).click();
```

---

# Best Practices

✅ Prefer `locator.hover()` over `page.hover()`.

✅ Use user-friendly locators like `getByRole()`, `getByText()`, and `getByLabel()` whenever possible.

✅ Verify the expected UI change after hovering using assertions.

✅ Avoid using `waitForTimeout()` before hovering.

✅ Use `force: true` only when absolutely required.

---

# Common Interview Questions

### Q1. What is the purpose of `hover()`?

**Answer:**

The `hover()` method moves the mouse pointer over an element without clicking it. It is commonly used to trigger hover effects such as menus and tooltips.

---

### Q2. Does `hover()` perform a click?

**Answer:**

No. It only moves the mouse pointer over the element. It does not click.

---

### Q3. When is `hover()` commonly used?

**Answer:**

- Navigation menus
- Submenus
- Tooltips
- Hidden buttons
- Hover animations

---

### Q4. Does Playwright automatically wait before hovering?

**Answer:**

Yes. Playwright automatically waits until the element is visible, stable, and ready for interaction.

---

### Q5. Can `hover()` be combined with `click()`?

**Answer:**

Yes. A common pattern is to hover over a menu to reveal additional options and then click one of them.

```javascript
await page.locator('#products').hover();

await page.locator('text=Software').click();
```

---

# Summary

| Method | Purpose |
|--------|---------|
| `hover()` | Moves the mouse pointer over an element |
| `force: true` | Forces the hover action |
| `toBeVisible()` | Verifies an element becomes visible after hovering |
| `locator.hover()` | Recommended approach |

---

# Key Points

- `hover()` moves the mouse pointer over an element without clicking.
- It is useful for menus, tooltips, hidden buttons, and hover-based interactions.
- Playwright automatically waits for the element before hovering.
- Verify the expected result after hovering using assertions.
- Prefer `locator.hover()` over `page.hover()` for better readability and maintainability.
