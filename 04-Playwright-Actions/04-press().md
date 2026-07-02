# ⌨️ Playwright Actions - Press

## 📌 Press Action

The `press()` method is used to simulate pressing a keyboard key on an element. It is commonly used to trigger keyboard events such as **Enter**, **Tab**, **Escape**, **Arrow Keys**, **Backspace**, and keyboard shortcuts like **Ctrl + A**.

The `press()` method first focuses on the element (if needed) and then sends the specified key press.

---

# Syntax

```javascript
await page.locator('locator').press('key');
```

or

```javascript
await page.press('locator', 'key');
```

> ✅ **Recommended:** Use `locator().press()` because it is more reliable, reusable, and supports Playwright's auto-waiting mechanism.

---

# Example 1: Press Enter

```javascript
import { test } from '@playwright/test';

test('Press Enter Key', async ({ page }) => {

    await page.goto('https://example.com');

    await page.locator('#search').fill('Playwright');

    await page.locator('#search').press('Enter');

});
```

---

# Example 2: Press Tab

Moves the keyboard focus to the next input field.

```javascript
await page.locator('#username').press('Tab');
```

---

# Example 3: Press Escape

Closes dialogs, popups, or cancels certain operations.

```javascript
await page.locator('#search').press('Escape');
```

---

# Example 4: Press Arrow Keys

Move through menus, dropdowns, or lists.

```javascript
await page.locator('#menu').press('ArrowDown');

await page.locator('#menu').press('ArrowUp');

await page.locator('#menu').press('ArrowRight');

await page.locator('#menu').press('ArrowLeft');
```

---

# Example 5: Press Backspace

Deletes one character before the cursor.

```javascript
await page.locator('#username').press('Backspace');
```

---

# Example 6: Press Delete

Deletes one character after the cursor.

```javascript
await page.locator('#username').press('Delete');
```

---

# Example 7: Press Space

Useful for buttons, checkboxes, or keyboard navigation.

```javascript
await page.locator('#checkbox').press('Space');
```

---

# Example 8: Press Function Keys

```javascript
await page.locator('#textbox').press('F1');

await page.locator('#textbox').press('F5');
```

---

# Keyboard Shortcuts

### Select All

**Windows / Linux**

```javascript
await page.locator('#username').press('Control+A');
```

**macOS**

```javascript
await page.locator('#username').press('Meta+A');
```

---

### Copy

```javascript
await page.locator('#username').press('Control+C');
```

---

### Paste

```javascript
await page.locator('#username').press('Control+V');
```

---

### Cut

```javascript
await page.locator('#username').press('Control+X');
```

---

# Press Multiple Keys

```javascript
await page.locator('#textbox').press('Shift+Tab');
```

```javascript
await page.locator('#textbox').press('Control+Shift+Home');
```

---

# Using `page.keyboard.press()`

You can also press keys using the keyboard API.

```javascript
await page.keyboard.press('Enter');
```

```javascript
await page.keyboard.press('Escape');
```

> Use this when the key press is not tied to a specific element.

---

# Verify After Press

```javascript
await page.locator('#search').fill('Playwright');

await page.locator('#search').press('Enter');

await expect(page).toHaveURL(/search/);
```

---

# Commonly Used Keys

| Key | Purpose |
|------|---------|
| `Enter` | Submit forms or perform searches |
| `Tab` | Move to the next field |
| `Shift+Tab` | Move to the previous field |
| `Escape` | Close dialogs or popups |
| `Backspace` | Delete previous character |
| `Delete` | Delete next character |
| `Space` | Activate buttons or checkboxes |
| `ArrowUp` | Move up |
| `ArrowDown` | Move down |
| `ArrowLeft` | Move left |
| `ArrowRight` | Move right |

---

# Best Practices

✅ Prefer `locator.press()` over `page.press()`.

✅ Use meaningful locators like `getByRole()`, `getByLabel()`, and `getByPlaceholder()`.

✅ Use `page.keyboard.press()` only when the action is not associated with a specific element.

✅ Verify the expected result after pressing a key using assertions.

✅ Avoid unnecessary `waitForTimeout()` before pressing keys.

---

# Common Interview Questions

### Q1. What is the purpose of `press()`?

**Answer:**

`press()` simulates pressing a keyboard key on an element, triggering the corresponding keyboard events.

---

### Q2. What is the difference between `locator.press()` and `page.keyboard.press()`?

**Answer:**

- `locator.press()` sends the key press to a specific element.
- `page.keyboard.press()` sends the key press to the currently focused element or active page.

---

### Q3. How do you submit a form using the keyboard?

**Answer:**

```javascript
await page.locator('#search').press('Enter');
```

---

### Q4. How do you move to the next input field?

**Answer:**

```javascript
await page.locator('#username').press('Tab');
```

---

### Q5. Can `press()` be used with keyboard shortcuts?

**Answer:**

Yes. It supports combinations such as:

```javascript
await page.locator('#username').press('Control+A');
await page.locator('#username').press('Control+C');
await page.locator('#username').press('Control+V');
```

---

# Summary

| Method | Purpose |
|--------|---------|
| `press('Enter')` | Press Enter key |
| `press('Tab')` | Move to next field |
| `press('Escape')` | Close popup or dialog |
| `press('Backspace')` | Delete previous character |
| `press('Delete')` | Delete next character |
| `press('Control+A')` | Select all text |
| `page.keyboard.press()` | Press a key globally |

---

# Key Points

- `press()` simulates keyboard input on an element.
- It supports single keys and keyboard shortcuts.
- Use `locator.press()` for element-specific interactions.
- Use `page.keyboard.press()` for global keyboard actions.
- Combine `press()` with assertions to verify the application's behavior after the key press.
