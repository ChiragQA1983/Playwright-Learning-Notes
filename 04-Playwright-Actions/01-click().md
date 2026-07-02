# 🖱️ Playwright Actions - Click & Double Click

## 📌 Click Action

The `click()` method is used to perform a mouse click on an element like a button, link, checkbox, radio button, or any clickable UI element.

### Syntax

```javascript
await page.locator('locator').click();
```

or

```javascript
await page.click('locator');
```

---

## Example 1: Click a Button

```javascript
import { test } from '@playwright/test';

test('Click Button Example', async ({ page }) => {

    await page.goto('https://example.com');

    await page.locator('#loginBtn').click();

});
```

---

## Example 2: Click Using Different Locators

### By ID

```javascript
await page.locator('#submit').click();
```

### By Text

```javascript
await page.getByText('Login').click();
```

### By Role

```javascript
await page.getByRole('button', { name: 'Submit' }).click();
```

### By Placeholder

```javascript
await page.getByPlaceholder('Search').click();
```

---

# Click Options

Playwright provides several useful click options.

### Delay Click

Waits before releasing the mouse button.

```javascript
await page.locator('#submit').click({
    delay: 500
});
```

---

### Force Click

Clicks even if Playwright thinks the element is not interactable.

```javascript
await page.locator('#submit').click({
    force: true
});
```

> ⚠️ Use only when necessary.

---

### Click with Mouse Button

Left Click (Default)

```javascript
await page.locator('#button').click();
```

Right Click

```javascript
await page.locator('#button').click({
    button: 'right'
});
```

Middle Click

```javascript
await page.locator('#button').click({
    button: 'middle'
});
```

---

### Click with Keyboard Modifier

Ctrl + Click

```javascript
await page.locator('#link').click({
    modifiers: ['Control']
});
```

Shift + Click

```javascript
await page.locator('#link').click({
    modifiers: ['Shift']
});
```

Alt + Click

```javascript
await page.locator('#link').click({
    modifiers: ['Alt']
});
```

---

## Click at Specific Position

Clicks at a particular coordinate inside an element.

```javascript
await page.locator('#canvas').click({
    position: {
        x: 100,
        y: 50
    }
});
```

---

# Multiple Clicks

Click multiple times.

```javascript
await page.locator('#button').click({
    clickCount: 3
});
```

---

# Double Click Action

The `dblclick()` method performs a double mouse click on an element.

### Syntax

```javascript
await page.locator('locator').dblclick();
```

or

```javascript
await page.dblclick('locator');
```

---

## Example

```javascript
import { test } from '@playwright/test';

test('Double Click Example', async ({ page }) => {

    await page.goto('https://example.com');

    await page.locator('#doubleClickBtn').dblclick();

});
```

---

## Double Click with Options

### Force Double Click

```javascript
await page.locator('#button').dblclick({
    force: true
});
```

---

### Delay

```javascript
await page.locator('#button').dblclick({
    delay: 300
});
```

---

### Double Click with Modifier

```javascript
await page.locator('#button').dblclick({
    modifiers: ['Control']
});
```

---

# Best Practices

✅ Prefer `locator.click()` over `page.click()`.

✅ Use Playwright Locators (`getByRole`, `getByText`, `getByLabel`) whenever possible.

✅ Avoid `force: true` unless absolutely required.

✅ Do not use unnecessary `waitForTimeout()` before clicking.

✅ Let Playwright automatically wait for the element to become visible and actionable.

✅ Use `dblclick()` only when the application specifically requires a double-click.

---

# Common Interview Questions

### Q1. What is the difference between `click()` and `dblclick()`?

**Answer:**

- `click()` performs a single mouse click.
- `dblclick()` performs two consecutive mouse clicks.

---

### Q2. What does `force: true` do?

**Answer:**

It forces Playwright to click the element even if it is covered, hidden, or not considered interactable.

---

### Q3. Does Playwright automatically wait before clicking?

**Answer:**

Yes. Playwright automatically waits until the element is:

- Visible
- Enabled
- Stable
- Receives pointer events

---

### Q4. Which is recommended?

```javascript
page.click('#submit');
```

or

```javascript
page.locator('#submit').click();
```

**Answer:**

`locator().click()` is recommended because it is more reliable, reusable, and supports Playwright's auto-waiting mechanism.

---

# Summary

| Method | Purpose |
|---------|---------|
| `click()` | Performs a single click |
| `dblclick()` | Performs a double click |
| `force: true` | Forces the click |
| `delay` | Adds delay before releasing the click |
| `button` | Left, Right, or Middle mouse button |
| `modifiers` | Ctrl, Shift, Alt, Meta keys |
| `position` | Click at specific coordinates |
| `clickCount` | Perform multiple clicks |
