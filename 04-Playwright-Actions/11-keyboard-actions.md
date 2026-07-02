# ⌨️ Playwright Actions - Keyboard Actions

## 📌 Keyboard Actions

Playwright provides the `keyboard` API to simulate real keyboard interactions such as typing text, pressing keys, using keyboard shortcuts, selecting text, copying, pasting, and navigating through the application.

Keyboard actions are useful for testing forms, search boxes, editors, shortcuts, and keyboard accessibility.

The Keyboard API is available through:

```javascript
page.keyboard
```

---

# Syntax

```javascript
await page.keyboard.action();
```

Examples:

```javascript
await page.keyboard.press('Enter');

await page.keyboard.type('Playwright');

await page.keyboard.down('Shift');

await page.keyboard.up('Shift');
```

---

# Example 1: Type Text

```javascript
import { test } from '@playwright/test';

test('Keyboard Type Example', async ({ page }) => {

    await page.goto('https://example.com');

    await page.locator('#username').click();

    await page.keyboard.type('Admin');

});
```

---

# Example 2: Press Enter

```javascript
await page.locator('#search').click();

await page.keyboard.type('Playwright');

await page.keyboard.press('Enter');
```

---

# Example 3: Press Tab

```javascript
await page.keyboard.press('Tab');
```

Moves the keyboard focus to the next element.

---

# Example 4: Press Escape

```javascript
await page.keyboard.press('Escape');
```

Used to close dialogs, popups, or cancel operations.

---

# Example 5: Press Arrow Keys

```javascript
await page.keyboard.press('ArrowUp');

await page.keyboard.press('ArrowDown');

await page.keyboard.press('ArrowLeft');

await page.keyboard.press('ArrowRight');
```

Useful for navigation in menus, dropdowns, and lists.

---

# Example 6: Press Backspace

```javascript
await page.keyboard.press('Backspace');
```

Deletes the previous character.

---

# Example 7: Press Delete

```javascript
await page.keyboard.press('Delete');
```

Deletes the next character.

---

# Example 8: Press Space

```javascript
await page.keyboard.press('Space');
```

Commonly used for buttons, checkboxes, and keyboard navigation.

---

# Example 9: Keyboard Shortcuts

### Select All

```javascript
await page.keyboard.press('Control+A');
```

---

### Copy

```javascript
await page.keyboard.press('Control+C');
```

---

### Paste

```javascript
await page.keyboard.press('Control+V');
```

---

### Cut

```javascript
await page.keyboard.press('Control+X');
```

---

### Undo

```javascript
await page.keyboard.press('Control+Z');
```

---

### Redo

```javascript
await page.keyboard.press('Control+Y');
```

---

# Example 10: Hold a Key

```javascript
await page.keyboard.down('Shift');

await page.keyboard.press('ArrowRight');

await page.keyboard.up('Shift');
```

Useful when testing keyboard selection.

---

# Example 11: Type with Delay

```javascript
await page.keyboard.type(
    'Playwright Automation',
    {
        delay: 100
    }
);
```

Each character is typed after a 100 ms delay.

---

# Example 12: Press Function Keys

```javascript
await page.keyboard.press('F1');

await page.keyboard.press('F5');

await page.keyboard.press('F12');
```

---

# Commonly Used Keys

| Key | Purpose |
|------|---------|
| Enter | Submit forms |
| Tab | Move to next field |
| Shift+Tab | Move to previous field |
| Escape | Close dialog |
| Backspace | Delete previous character |
| Delete | Delete next character |
| Space | Select checkbox/button |
| Arrow Keys | Navigation |
| Home | Move cursor to beginning |
| End | Move cursor to end |
| PageUp | Scroll up |
| PageDown | Scroll down |

---

# Difference Between `keyboard.type()` and `fill()`

| keyboard.type() | fill() |
|-----------------|---------|
| Types one character at a time | Sets the entire value at once |
| Simulates real typing | Does not simulate typing |
| Supports typing delay | No typing delay |
| Triggers keyboard events | Primarily updates the input value |
| Slower | Faster |

---

# Difference Between `keyboard.press()` and `locator.press()`

| keyboard.press() | locator.press() |
|------------------|-----------------|
| Sends the key to the currently focused element | Sends the key to a specific element |
| Requires focus | Automatically focuses the element if needed |
| Used for global keyboard actions | Used for element-specific actions |

---

# Real-Time Use Cases

### Submit Login Form

```javascript
await page.keyboard.type('admin');

await page.keyboard.press('Tab');

await page.keyboard.type('Admin@123');

await page.keyboard.press('Enter');
```

---

### Search Product

```javascript
await page.locator('#search').click();

await page.keyboard.type('Laptop');

await page.keyboard.press('Enter');
```

---

### Close Popup

```javascript
await page.keyboard.press('Escape');
```

---

# Best Practices

✅ Use `locator.press()` when the action belongs to a specific element.

✅ Use `page.keyboard.press()` for global keyboard actions.

✅ Use `keyboard.type()` when you need to simulate real user typing.

✅ Use `fill()` instead of `keyboard.type()` when typing behavior is not important.

✅ Verify the application's response using assertions.

---

# Common Interview Questions

### Q1. What is the Keyboard API in Playwright?

**Answer:**

The Keyboard API simulates keyboard interactions such as typing text, pressing keys, and using keyboard shortcuts.

---

### Q2. What is the difference between `keyboard.type()` and `fill()`?

**Answer:**

- `keyboard.type()` types one character at a time and triggers keyboard events.
- `fill()` replaces the input value directly and is generally faster.

---

### Q3. When should you use `page.keyboard.press()`?

**Answer:**

Use it when the key press is not associated with a specific element or when the desired element already has focus.

---

### Q4. How do you simulate keyboard shortcuts?

**Answer:**

```javascript
await page.keyboard.press('Control+A');

await page.keyboard.press('Control+C');

await page.keyboard.press('Control+V');
```

---

### Q5. How do you hold a key while pressing another key?

**Answer:**

```javascript
await page.keyboard.down('Shift');

await page.keyboard.press('ArrowRight');

await page.keyboard.up('Shift');
```

---

# Summary

| Method | Purpose |
|--------|---------|
| `keyboard.type()` | Type text character by character |
| `keyboard.press()` | Press a keyboard key |
| `keyboard.down()` | Hold a key |
| `keyboard.up()` | Release a held key |
| `keyboard.insertText()` | Insert text without generating key press events |

---

# Key Points

- The Keyboard API simulates real keyboard interactions.
- Use `keyboard.type()` to mimic actual typing.
- Use `keyboard.press()` to press individual keys or keyboard shortcuts.
- Use `keyboard.down()` and `keyboard.up()` for key combinations.
- Prefer `locator.press()` for element-specific interactions and `page.keyboard.press()` for global keyboard actions.
