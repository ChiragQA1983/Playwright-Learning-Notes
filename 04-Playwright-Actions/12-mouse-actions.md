# 🖱️ Playwright Actions - Mouse Actions

## 📌 Mouse Actions

Playwright provides the **Mouse API** to simulate real mouse interactions such as moving the cursor, clicking, double-clicking, right-clicking, pressing mouse buttons, releasing mouse buttons, and scrolling using the mouse wheel.

The Mouse API is useful for testing drag-and-drop operations, canvas drawings, custom sliders, image editors, maps, games, and applications that rely on mouse events.

The Mouse API is available through:

```javascript
page.mouse
```

---

# Syntax

```javascript
await page.mouse.action();
```

Examples:

```javascript
await page.mouse.move(x, y);

await page.mouse.click(x, y);

await page.mouse.dblclick(x, y);

await page.mouse.down();

await page.mouse.up();

await page.mouse.wheel(deltaX, deltaY);
```

---

# Example 1: Move Mouse Pointer

Moves the mouse pointer to the specified coordinates.

```javascript
import { test } from '@playwright/test';

test('Mouse Move Example', async ({ page }) => {

    await page.goto('https://example.com');

    await page.mouse.move(300, 200);

});
```

---

# Example 2: Mouse Click

Clicks at the specified screen coordinates.

```javascript
await page.mouse.click(300, 200);
```

---

# Example 3: Double Click

```javascript
await page.mouse.dblclick(300, 200);
```

---

# Example 4: Right Click

```javascript
await page.mouse.click(300, 200, {

    button: 'right'

});
```

---

# Example 5: Middle Click

```javascript
await page.mouse.click(300, 200, {

    button: 'middle'

});
```

---

# Example 6: Mouse Down

Presses and holds the left mouse button.

```javascript
await page.mouse.down();
```

---

# Example 7: Mouse Up

Releases the pressed mouse button.

```javascript
await page.mouse.up();
```

---

# Example 8: Drag and Drop Using Mouse API

```javascript
const source = page.locator('#source');

const target = page.locator('#target');

await source.hover();

await page.mouse.down();

await target.hover();

await page.mouse.up();
```

> Use this approach when `locator.dragTo()` is not supported by the application.

---

# Example 9: Draw on Canvas

```javascript
await page.mouse.move(200, 200);

await page.mouse.down();

await page.mouse.move(400, 200);

await page.mouse.move(400, 400);

await page.mouse.up();
```

Useful for testing signature pads, drawing applications, and whiteboards.

---

# Example 10: Scroll Using Mouse Wheel

Scroll down

```javascript
await page.mouse.wheel(0, 500);
```

Scroll up

```javascript
await page.mouse.wheel(0, -500);
```

Horizontal scroll

```javascript
await page.mouse.wheel(500, 0);
```

---

# Example 11: Smooth Mouse Movement

```javascript
await page.mouse.move(
    500,
    300,
    {
        steps: 20
    }
);
```

The `steps` option moves the mouse gradually instead of jumping directly to the destination.

---

# Mouse API Methods

| Method | Purpose |
|---------|---------|
| `move()` | Move mouse pointer |
| `click()` | Perform mouse click |
| `dblclick()` | Perform double click |
| `down()` | Press mouse button |
| `up()` | Release mouse button |
| `wheel()` | Scroll using mouse wheel |

---

# Difference Between Locator Actions and Mouse API

| Locator API | Mouse API |
|--------------|-----------|
| Works with elements | Works with screen coordinates |
| Auto-waits for elements | No auto-waiting |
| Easier to maintain | More manual control |
| Recommended for UI elements | Best for canvas, maps, games, sliders |

---

# Real-Time Use Cases

### Drag a Slider

```javascript
await page.mouse.move(250, 300);

await page.mouse.down();

await page.mouse.move(450, 300);

await page.mouse.up();
```

---

### Draw Signature

```javascript
await page.mouse.move(200, 200);

await page.mouse.down();

await page.mouse.move(220, 210);

await page.mouse.move(250, 230);

await page.mouse.up();
```

---

### Scroll to Bottom

```javascript
await page.mouse.wheel(0, 1000);
```

---

### Open Context Menu

```javascript
await page.mouse.click(400, 250, {

    button: 'right'

});
```

---

# Best Practices

✅ Prefer Locator methods (`click()`, `hover()`, `dragTo()`) for standard UI interactions.

✅ Use the Mouse API only when coordinate-based interactions are required.

✅ Use `steps` for smoother mouse movement in drawing or drag operations.

✅ Verify application behavior using assertions after mouse actions.

✅ Avoid hardcoded coordinates unless the UI layout is fixed.

---

# Common Interview Questions

### Q1. What is the Mouse API in Playwright?

**Answer:**

The Mouse API simulates mouse interactions such as moving the pointer, clicking, dragging, releasing buttons, and scrolling.

---

### Q2. When should you use the Mouse API?

**Answer:**

Use the Mouse API for:

- Canvas drawing
- Maps
- Sliders
- Games
- Custom drag-and-drop implementations
- Coordinate-based interactions

---

### Q3. What is the difference between `locator.click()` and `page.mouse.click()`?

**Answer:**

- `locator.click()` works with elements and automatically waits for them to become actionable.
- `page.mouse.click()` clicks at specific screen coordinates and does not provide element-based auto-waiting.

---

### Q4. What is the purpose of the `steps` option in `mouse.move()`?

**Answer:**

The `steps` option moves the mouse gradually, simulating smooth cursor movement instead of jumping directly to the destination.

Example:

```javascript
await page.mouse.move(500, 300, {

    steps: 20

});
```

---

### Q5. How do you scroll using the Mouse API?

**Answer:**

```javascript
await page.mouse.wheel(0, 500);
```

The first value controls horizontal scrolling (`deltaX`), and the second value controls vertical scrolling (`deltaY`).

---

# Summary

| Method | Purpose |
|--------|---------|
| `mouse.move()` | Move the mouse pointer |
| `mouse.click()` | Click at coordinates |
| `mouse.dblclick()` | Double-click at coordinates |
| `mouse.down()` | Press mouse button |
| `mouse.up()` | Release mouse button |
| `mouse.wheel()` | Scroll using the mouse wheel |

---

# Key Points

- The Mouse API is used for coordinate-based mouse interactions.
- It is ideal for canvas drawing, sliders, maps, games, and custom drag-and-drop.
- Locator-based actions are preferred for standard web elements because they are easier to maintain and include auto-waiting.
- Use `mouse.wheel()` for horizontal and vertical scrolling.
- Combine mouse actions with assertions to verify the expected application behavior.
