# 🎯 CSS Selector in Playwright

## 📖 What is a CSS Selector?

A **CSS Selector (Cascading Style Sheets Selector)** is a pattern used to locate HTML elements on a web page. In Playwright, CSS selectors are commonly used with the `locator()` method to identify and interact with elements.

CSS selectors are generally **faster, cleaner, and easier to maintain** than XPath.

---

# Why Use CSS Selectors?

- Fast element identification
- Easy to read and write
- Supported by all modern browsers
- Ideal for automation testing
- Less complex than XPath
- Recommended when DOM traversal is not required

---

# Syntax

```javascript
await page.locator("css-selector");
```

Example:

```javascript
await page.locator("#username").fill("Admin");
```

---

# HTML Example

```html
<form id="loginForm">

    <input
        id="username"
        class="input-field"
        type="text"
        name="username"
        placeholder="Enter Username">

    <input
        id="password"
        class="input-field"
        type="password">

    <button
        id="loginBtn"
        class="btn btn-primary">
        Login
    </button>

</form>
```

---

# CSS Selector Types

## 1. ID Selector

Selects an element using its **id** attribute.

### Syntax

```css
#id
```

### Example

```javascript
await page.locator("#username").fill("Admin");
```

HTML

```html
<input id="username">
```

---

## 2. Class Selector

Selects elements using their class attribute.

### Syntax

```css
.className
```

Example

```javascript
await page.locator(".btn-primary").click();
```

HTML

```html
<button class="btn-primary">
```

---

## 3. Tag Selector

Selects elements by HTML tag.

Example

```javascript
await page.locator("input");
```

HTML

```html
<input>
```

---

## 4. Attribute Selector

Selects elements using attributes.

Example

```javascript
await page.locator("[type='text']");
```

HTML

```html
<input type="text">
```

---

## 5. Multiple Attributes

```javascript
await page.locator("input[type='text'][name='username']");
```

HTML

```html
<input type="text" name="username">
```

---

## 6. Parent Child Selector

Selects child elements inside a parent.

Example

```javascript
await page.locator("form input");
```

HTML

```html
<form>
    <input>
</form>
```

---

## 7. Direct Child Selector (>)

Selects only direct children.

Example

```javascript
await page.locator("ul > li");
```

HTML

```html
<ul>
    <li>Apple</li>
</ul>
```

---

## 8. Descendant Selector

Selects all descendants.

Example

```javascript
await page.locator("table tr td");
```

---

## 9. First Child

Example

```javascript
await page.locator("li:first-child");
```

---

## 10. Last Child

Example

```javascript
await page.locator("li:last-child");
```

---

## 11. nth-child()

Selects an element based on position.

Example

```javascript
await page.locator("li:nth-child(3)");
```

---

## 12. nth-of-type()

Example

```javascript
await page.locator("tr:nth-of-type(2)");
```

---

## 13. Universal Selector

Selects every element.

```javascript
page.locator("*")
```

---

## 14. Multiple Selectors

```javascript
page.locator("input, button")
```

---

## 15. Adjacent Sibling (+)

Selects the immediate sibling.

Example

```javascript
page.locator("label + input")
```

---

## 16. General Sibling (~)

Example

```javascript
page.locator("label ~ input")
```

---

# Real-Time Examples

## Fill Username

```javascript
await page.locator("#username").fill("Admin");
```

---

## Fill Password

```javascript
await page.locator("#password").fill("Admin123");
```

---

## Click Login Button

```javascript
await page.locator(".btn-primary").click();
```

---

## Click Search Button

```javascript
await page.locator("[type='submit']").click();
```

---

## Select First Product

```javascript
await page.locator(".product-item:first-child").click();
```

---

## Select Third Row

```javascript
await page.locator("tbody tr:nth-child(3)");
```

---

# CSS Selector Priority

Recommended order:

1. ID
2. data-testid
3. Name
4. Class
5. Attribute
6. Tag

---

# Advantages

- Very fast
- Easy to maintain
- Readable
- Supported by all browsers
- Less typing than XPath
- Better performance

---

# Limitations

- Cannot move from child to parent
- Cannot search by visible text
- Less flexible than XPath

---

# CSS vs XPath

| CSS Selector | XPath |
|--------------|--------|
| Faster | Slightly slower |
| Easy syntax | More complex |
| Cannot traverse upward | Can traverse upward |
| Better readability | More flexible |
| Recommended when possible | Use when CSS cannot locate the element |

---

# Best Practices

✅ Prefer ID selectors.

```javascript
page.locator("#loginBtn")
```

---

✅ Use data-testid whenever available.

```javascript
page.locator("[data-testid='login']")
```

---

✅ Keep selectors short.

Good

```javascript
#username
```

Bad

```javascript
body > div > div > form > input
```

---

✅ Avoid long CSS chains.

---

✅ Avoid dynamic classes.

Bad

```css
.css-123ab
```

Good

```css
#username
```

---

# Common Mistakes

❌ Using long CSS paths

❌ Using dynamic class names

❌ Depending on element position

❌ Writing unreadable selectors

---

# Interview Questions

### Q1 What is a CSS Selector?

A CSS Selector identifies HTML elements using IDs, classes, attributes, tags, and relationships.

---

### Q2 Why is CSS faster than XPath?

Because browsers have native CSS selector engines optimized for performance.

---

### Q3 Can CSS move from child to parent?

No.

XPath supports parent traversal, but CSS does not.

---

### Q4 Which locator should be preferred in Playwright?

Preferred order:

1. getByRole()
2. getByLabel()
3. getByPlaceholder()
4. getByText()
5. getByTestId()
6. CSS Selector
7. XPath

---

### Q5 When should XPath be used instead of CSS?

Use XPath when:

- Traversing to parent elements
- Using sibling axes
- Complex DOM navigation
- CSS cannot uniquely identify the element

---

# Practice Exercise

Write CSS selectors for:

1. Username textbox
2. Password textbox
3. Login button
4. Logout button
5. Search box
6. Search button
7. First product
8. Last product
9. Third row of a table
10. Checkbox

---

# Summary

- CSS selectors are fast and easy to maintain.
- Prefer CSS over XPath whenever possible.
- Use short and stable selectors.
- Avoid dynamic classes and long selector chains.
- In Playwright, use user-facing locators (`getByRole`, `getByLabel`, etc.) before falling back to CSS selectors.
