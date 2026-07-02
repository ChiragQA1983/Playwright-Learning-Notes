# 📜 Playwright Actions - Scroll

## 📌 Scroll Action

Scrolling is used to bring elements into view, navigate long web pages, load lazy-loaded content, and interact with elements that are outside the visible viewport.

Playwright provides multiple ways to scroll depending on the scenario.

---

# Scroll Methods in Playwright

| Method | Purpose |
|---------|---------|
| `locator.scrollIntoViewIfNeeded()` | Scroll until an element becomes visible |
| `page.mouse.wheel()` | Scroll using the mouse wheel |
| `window.scrollTo()` | Scroll to a specific page position |
| `window.scrollBy()` | Scroll relative to the current position |

---

# Method 1: scrollIntoViewIfNeeded()

## 📌 Description

The `scrollIntoViewIfNeeded()` method automatically scrolls the page until the target element is visible.

This is the **recommended** approach because it is element-based and automatically waits for the element.

---

# Syntax

```javascript
await page.locator('locator').scrollIntoViewIfNeeded();
```

---

# Example 1: Scroll to an Element

```javascript
import { test } from '@playwright/test';

test('Scroll to Element', async ({ page }) => {

    await page.goto('https://example.com');

    await page.locator('#footer')
        .scrollIntoViewIfNeeded();

});
```

---

# Example 2: Scroll and Click

```javascript
await page.locator('#submitButton')
    .scrollIntoViewIfNeeded();

await page.locator('#submitButton')
    .click();
```

---

# Method 2: Mouse Wheel Scroll

## 📌 Description

Simulates scrolling using the mouse wheel.

---

### Scroll Down

```javascript
await page.mouse.wheel(0, 500);
```

---

### Scroll Up

```javascript
await page.mouse.wheel(0, -500);
```

---

### Horizontal Scroll

```javascript
await page.mouse.wheel(500, 0);
```

---

# Method 3: window.scrollTo()

## 📌 Description

Scrolls the page to an absolute position.

---

### Scroll to Bottom

```javascript
await page.evaluate(() => {

    window.scrollTo(
        0,
        document.body.scrollHeight
    );

});
```

---

### Scroll to Top

```javascript
await page.evaluate(() => {

    window.scrollTo(0, 0);

});
```

---

### Scroll to Specific Position

```javascript
await page.evaluate(() => {

    window.scrollTo(0, 800);

});
```

---

# Method 4: window.scrollBy()

## 📌 Description

Scrolls relative to the current position.

---

### Scroll Down

```javascript
await page.evaluate(() => {

    window.scrollBy(0, 500);

});
```

---

### Scroll Up

```javascript
await page.evaluate(() => {

    window.scrollBy(0, -500);

});
```

---

### Horizontal Scroll

```javascript
await page.evaluate(() => {

    window.scrollBy(500, 0);

});
```

---

# Example: Infinite Scrolling

Many modern websites load more data while scrolling.

```javascript
while (true) {

    const previousHeight =
        await page.evaluate(() => document.body.scrollHeight);

    await page.mouse.wheel(0, 1000);

    await page.waitForTimeout(1000);

    const currentHeight =
        await page.evaluate(() => document.body.scrollHeight);

    if (previousHeight === currentHeight)
        break;

}
```

> ⚠️ Prefer waiting for a specific element or network response instead of `waitForTimeout()` in production tests. The timeout is shown here only for demonstration.

---

# Example: Lazy Loading Images

```javascript
await page.locator('#image100')
    .scrollIntoViewIfNeeded();

await expect(
    page.locator('#image100')
).toBeVisible();
```

---

# Example: Scroll Inside a Container

```javascript
await page.locator('.scrollable-container')
    .evaluate(element => {

        element.scrollTop = 500;

    });
```

---

# Example: Scroll to Bottom and Verify

```javascript
await page.evaluate(() => {

    window.scrollTo(
        0,
        document.body.scrollHeight
    );

});

await expect(
    page.locator('#footer')
).toBeVisible();
```

---

# Difference Between Scroll Methods

| Method | Best Use Case |
|----------|---------------|
| `scrollIntoViewIfNeeded()` | Scroll to a specific element |
| `mouse.wheel()` | Simulate user scrolling |
| `window.scrollTo()` | Scroll to an absolute page position |
| `window.scrollBy()` | Scroll relative to the current position |

---

# Real-Time Use Cases

### Scroll to Footer

```javascript
await page.locator('#footer')
    .scrollIntoViewIfNeeded();
```

---

### Load Infinite Products

```javascript
await page.mouse.wheel(0, 1500);
```

---

### Scroll Before Clicking

```javascript
await page.locator('#saveButton')
    .scrollIntoViewIfNeeded();

await page.locator('#saveButton')
    .click();
```

---

### Scroll to Top

```javascript
await page.evaluate(() => {

    window.scrollTo(0, 0);

});
```

---

# Best Practices

✅ Prefer `scrollIntoViewIfNeeded()` when interacting with specific elements.

✅ Use `mouse.wheel()` when testing user scrolling behavior.

✅ Avoid using `waitForTimeout()` after scrolling unless absolutely necessary.

✅ Verify the target element after scrolling using assertions.

✅ Use JavaScript scrolling only when locator-based scrolling is not suitable.

---

# Common Interview Questions

### Q1. What is the recommended way to scroll to an element in Playwright?

**Answer:**

```javascript
await page.locator('#footer')
    .scrollIntoViewIfNeeded();
```

It is element-based, reliable, and supports Playwright's auto-waiting.

---

### Q2. What is the difference between `scrollTo()` and `scrollBy()`?

**Answer:**

- `scrollTo()` scrolls to an absolute position.
- `scrollBy()` scrolls relative to the current position.

---

### Q3. How do you simulate mouse wheel scrolling?

**Answer:**

```javascript
await page.mouse.wheel(0, 500);
```

---

### Q4. How do you handle infinite scrolling?

**Answer:**

Scroll repeatedly until the page height no longer increases or until the desired content appears.

---

### Q5. Which scrolling method is recommended?

**Answer:**

`locator.scrollIntoViewIfNeeded()` is recommended because it automatically scrolls the page until the target element is visible and ready for interaction.

---

# Summary

| Method | Purpose |
|--------|---------|
| `scrollIntoViewIfNeeded()` | Scroll to an element |
| `mouse.wheel()` | Simulate mouse wheel scrolling |
| `window.scrollTo()` | Scroll to an absolute position |
| `window.scrollBy()` | Scroll relative to the current position |
| `evaluate()` | Execute JavaScript-based scrolling |

---

# Key Points

- Playwright provides multiple ways to scroll depending on the use case.
- `scrollIntoViewIfNeeded()` is the preferred method for interacting with elements.
- `mouse.wheel()` simulates real user scrolling.
- `window.scrollTo()` and `window.scrollBy()` are useful for page-level scrolling.
- Always verify the expected result after scrolling using assertions.
