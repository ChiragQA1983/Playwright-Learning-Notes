# 🎯 Playwright Actions - Drag and Drop

## 📌 Drag and Drop Action

The `dragTo()` method is used to **drag an element from a source location and drop it onto a target element**. It simulates a real user dragging an item with the mouse and releasing it over another element.

This action is commonly used for Kanban boards, sortable lists, file organizers, dashboards, calendars, and UI builders.

Playwright automatically waits for both the source and target elements to become visible, stable, and ready before performing the drag-and-drop action.

---

# Syntax

```javascript
await page.locator('sourceLocator').dragTo(
    page.locator('targetLocator')
);
```

> ✅ **Recommended:** Use `locator.dragTo()` because it is more reliable, readable, and supports Playwright's auto-waiting mechanism.

---

# Example HTML

```html
<div id="source">Drag Me</div>

<div id="target">Drop Here</div>
```

---

# Example 1: Basic Drag and Drop

```javascript
import { test } from '@playwright/test';

test('Drag and Drop Example', async ({ page }) => {

    await page.goto('https://example.com');

    const source = page.locator('#source');

    const target = page.locator('#target');

    await source.dragTo(target);

});
```

---

# Example 2: Drag Using Different Locators

### By ID

```javascript
await page.locator('#source')
    .dragTo(page.locator('#target'));
```

### By Text

```javascript
await page.getByText('Drag Me')
    .dragTo(page.getByText('Drop Here'));
```

### By Role

```javascript
await page.getByRole('listitem', {
    name: 'Task 1'
}).dragTo(
    page.getByRole('list', {
        name: 'Completed Tasks'
    })
);
```

### By CSS Selector

```javascript
await page.locator('.drag-item')
    .dragTo(page.locator('.drop-zone'));
```

---

# Example 3: Drag Between Columns

```javascript
const todo = page.locator('#todoTask');

const completed = page.locator('#completedColumn');

await todo.dragTo(completed);
```

---

# Verify Drag and Drop

```javascript
await source.dragTo(target);

await expect(target).toContainText('Drag Me');
```

> Adjust the assertion based on your application's behavior.

---

# Drag Multiple Elements

```javascript
await page.locator('#item1')
    .dragTo(page.locator('#target'));

await page.locator('#item2')
    .dragTo(page.locator('#target'));

await page.locator('#item3')
    .dragTo(page.locator('#target'));
```

---

# Drag Using Mouse Actions (Alternative)

If an application does not support `dragTo()`, you can use the mouse API.

```javascript
const source = page.locator('#source');

const target = page.locator('#target');

await source.hover();

await page.mouse.down();

await target.hover();

await page.mouse.up();
```

> Use this approach only when `dragTo()` does not work because of custom drag-and-drop implementations.

---

# Drag with Position

You can specify exact positions inside the source and target elements.

```javascript
await page.locator('#source').dragTo(
    page.locator('#target'),
    {
        sourcePosition: {
            x: 20,
            y: 20
        },
        targetPosition: {
            x: 80,
            y: 40
        }
    }
);
```

---

# Wait Before Dragging

Playwright automatically waits until both elements are:

- Visible
- Stable
- Enabled
- Ready for interaction

```javascript
await source.dragTo(target);
```

No explicit wait is required in most cases.

---

# Difference Between `dragTo()` and Mouse Actions

| Feature | `dragTo()` | Mouse API |
|----------|------------|-----------|
| Built-in drag and drop | ✅ Yes | ❌ Manual implementation |
| Easy to use | ✅ Yes | ❌ More code required |
| Auto waiting | ✅ Yes | ❌ Manual handling may be needed |
| Recommended | ✅ Yes | ⚠️ Only for special cases |

---

# Real-Time Use Cases

### Move a Kanban Card

```javascript
await page.locator('#task1')
    .dragTo(page.locator('#doneColumn'));
```

---

### Reorder List Items

```javascript
await page.locator('#item1')
    .dragTo(page.locator('#item5'));
```

---

### Move Widgets on Dashboard

```javascript
await page.locator('#salesWidget')
    .dragTo(page.locator('#dashboardArea'));
```

---

# Best Practices

✅ Prefer `locator.dragTo()` over manual mouse operations.

✅ Use stable locators like `getByRole()`, `getByText()`, or unique IDs.

✅ Verify the result after dragging using assertions.

✅ Avoid `waitForTimeout()` before drag-and-drop.

✅ Use the Mouse API only if the application uses a custom drag-and-drop implementation that `dragTo()` cannot handle.

---

# Common Interview Questions

### Q1. What is the purpose of `dragTo()`?

**Answer:**

`dragTo()` is used to drag an element from a source location and drop it onto a target element.

---

### Q2. Does Playwright automatically wait before performing drag-and-drop?

**Answer:**

Yes. Playwright automatically waits until both the source and target elements are visible, stable, enabled, and ready for interaction.

---

### Q3. When should you use the Mouse API instead of `dragTo()`?

**Answer:**

Use the Mouse API when working with custom drag-and-drop implementations that do not respond correctly to `dragTo()`.

---

### Q4. How do you verify that drag-and-drop was successful?

**Answer:**

Use assertions based on your application's behavior, such as checking text, element position, or DOM changes.

```javascript
await expect(target).toContainText('Drag Me');
```

---

### Q5. Which approach is recommended?

**Answer:**

`locator.dragTo()` is the recommended approach because it is simpler, more readable, and supports Playwright's built-in auto-waiting.

---

# Summary

| Method | Purpose |
|--------|---------|
| `dragTo()` | Drag an element and drop it onto another element |
| `sourcePosition` | Specify the drag starting position |
| `targetPosition` | Specify the drop position |
| `page.mouse.down()` | Press the mouse button |
| `page.mouse.up()` | Release the mouse button |

---

# Key Points

- `dragTo()` is Playwright's built-in method for drag-and-drop operations.
- It automatically waits for the source and target elements to become ready.
- It is commonly used for Kanban boards, sortable lists, dashboards, and calendars.
- Use assertions to verify that the drag-and-drop operation completed successfully.
- Prefer `locator.dragTo()` over manual mouse actions whenever possible.
