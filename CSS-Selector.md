# 🎯 CSS Selector in Playwright

## What is CSS Selector?

A CSS Selector is used to locate HTML elements based on their attributes, classes, IDs, hierarchy, and relationships.

Playwright supports CSS selectors using the `locator()` method.

---

# Syntax

```javascript
await page.locator("css-selector");
```

Example

```javascript
await page.locator("#username").fill("Admin");
```

---

# Common CSS Selectors

## ID

```javascript
page.locator("#username")
```

HTML

```html
<input id="username">
```

---

## Class

```javascript
page.locator(".login-btn")
```

HTML

```html
<button class="login-btn">
```

---

## Tag Name

```javascript
page.locator("input")
```

---

## Attribute

```javascript
page.locator("[type='text']")
```

---

## Multiple Attributes

```javascript
page.locator("input[type='text'][name='username']")
```

---

## Parent Child

```javascript
page.locator("form input")
```

---

## Direct Child

```javascript
page.locator("ul > li")
```

---

## First Child

```javascript
page.locator("li:first-child")
```

---

## Last Child

```javascript
page.locator("li:last-child")
```

---

## nth Child

```javascript
page.locator("li:nth-child(3)")
```

---

# Advantages

✔ Fast

✔ Readable

✔ Recommended over XPath

✔ Easy Maintenance

---

# Limitations

Cannot travel upward in DOM.

---

# Best Practices

✅ Prefer ID

✅ Prefer Data-TestId

✅ Keep selectors short

❌ Avoid long CSS chains

---

# Interview Questions

Q1 Why CSS is faster than XPath?

Q2 Difference between CSS and XPath?

Q3 Can CSS travel from child to parent?

Answer:
No.

---

# Practice

Locate

- Username
- Password
- Login Button
- Logout Button

using CSS selectors.
