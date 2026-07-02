# 🎯 XPath in Playwright

## What is XPath?

XPath (XML Path Language) is used to locate elements by navigating the HTML DOM.

Playwright supports XPath through the `locator()` method.

---

# Syntax

```javascript
await page.locator("//button");
```

---

# Absolute XPath

```javascript
/html/body/div/input
```

❌ Not Recommended

---

# Relative XPath

```javascript
//input[@id='username']
```

✅ Recommended

---

# XPath by Attribute

```javascript
//input[@id='username']
```

---

# XPath by Text

```javascript
//button[text()='Login']
```

---

# Contains

```javascript
//button[contains(text(),'Login')]
```

---

# Starts With

```javascript
//input[starts-with(@id,'user')]
```

---

# Multiple Attributes

```javascript
//input[@id='username' and @type='text']
```

---

# Parent

```javascript
//input/parent::div
```

---

# Child

```javascript
//div/input
```

---

# Following

```javascript
//label/following::input
```

---

# Following Sibling

```javascript
//label/following-sibling::input
```

---

# Preceding

```javascript
//input/preceding::label
```

---

# Last

```javascript
(//button)[last()]
```

---

# Position

```javascript
(//button)[2]
```

---

# Advantages

✔ Flexible

✔ Powerful

✔ Supports DOM traversal

---

# Limitations

❌ Slower than CSS

❌ Long XPath is difficult to maintain

---

# Best Practices

✔ Prefer Relative XPath

✔ Avoid Absolute XPath

✔ Use contains()

✔ Keep XPath short

---

# Interview Questions

Q1 Difference between Relative and Absolute XPath?

Q2 Which is faster, CSS or XPath?

Q3 Why avoid Absolute XPath?

---

# Practice

Locate

- Login Button
- Username
- Password
- Remember Me Checkbox

using XPath.
