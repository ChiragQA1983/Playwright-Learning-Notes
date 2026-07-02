# 🌑 Shadow DOM in Playwright

## 📖 What is Shadow DOM?

**Shadow DOM** is a web standard that allows developers to encapsulate a part of the DOM (Document Object Model) so that its internal structure, styles, and behavior are isolated from the main document.

It is commonly used in **Web Components** to prevent style and JavaScript conflicts.

A Shadow DOM creates a **separate DOM tree** attached to a regular HTML element called the **Shadow Host**.

---

# Why is Shadow DOM Used?

Shadow DOM provides:

- Encapsulation
- Style Isolation
- DOM Isolation
- Reusable Components
- Better Code Organization

It ensures that CSS and JavaScript inside a component do not interfere with the rest of the application.

---

# Real-World Applications

Shadow DOM is widely used in:

- Material UI
- Ionic Framework
- Salesforce Lightning
- Polymer
- Lit
- Shoelace Components
- Many modern web applications

---

# DOM Structure

Normal DOM

```html
<body>

<div>

<button>Login</button>

</div>

</body>
```

---

Shadow DOM

```html
<body>

<login-component>

#shadow-root

<button>Login</button>

</login-component>

</body>
```

Here,

- `login-component` → Shadow Host
- `#shadow-root` → Shadow Root
- `button` → Shadow Element

---

# Types of Shadow DOM

## 1. Open Shadow DOM

Accessible from JavaScript.

```javascript
element.shadowRoot
```

Playwright can automatically locate elements inside an **open Shadow DOM**.

---

## 2. Closed Shadow DOM

Not accessible.

```javascript
element.shadowRoot
```

returns

```javascript
null
```

Closed Shadow DOM cannot be accessed directly using Playwright locators.

---

# Shadow DOM Terminology

| Term | Description |
|------|-------------|
| Shadow Host | Element that owns the shadow root |
| Shadow Root | Root node of the shadow tree |
| Shadow Tree | Hidden DOM inside the component |
| Shadow Boundary | Boundary between normal DOM and Shadow DOM |

---

# Does Playwright Support Shadow DOM?

✅ Yes.

One of Playwright's biggest advantages is that it **automatically pierces open Shadow DOM**.

Unlike Selenium, Playwright usually does **not** require switching context for open Shadow DOM elements.

---

# Basic Example

HTML

```html
<custom-login>

#shadow-root

<input id="username">

</custom-login>
```

Playwright

```javascript
await page.locator("#username").fill("Admin");
```

No extra Shadow DOM API is required for an **open** shadow root.

---

# Example 2

```javascript
await page.getByPlaceholder("Username").fill("Admin");
```

Playwright automatically searches inside the open Shadow DOM.

---

# Example 3

```javascript
await page.getByRole("button", {
    name: "Login"
}).click();
```

---

# Nested Shadow DOM

HTML

```text
app-root
   |
   +-- shadow-root
         |
         +-- login-component
                 |
                 +-- shadow-root
                        |
                        +-- button
```

Playwright automatically traverses multiple levels of **open** shadow roots.

Example

```javascript
await page.getByRole("button", {
    name: "Login"
}).click();
```

---

# Using locator()

```javascript
await page
.locator("custom-login")
.locator("#username")
.fill("Admin");
```

---

# Chaining Example

```javascript
await page
.locator("user-card")
.locator("button")
.click();
```

---

# Using getByRole()

```javascript
await page
.getByRole("button", {
    name: "Submit"
})
.click();
```

Works inside open Shadow DOM.

---

# Using getByText()

```javascript
await page
.getByText("Welcome")
.click();
```

---

# Using getByLabel()

```javascript
await page
.getByLabel("Email")
.fill("abc@gmail.com");
```

---

# Real-Time Example

Suppose an application uses Material UI.

HTML

```html
<material-login>

#shadow-root

<input id="email">

<button>Login</button>

</material-login>
```

Playwright

```javascript
await page.locator("#email").fill("admin@gmail.com");

await page.getByRole("button", {
    name: "Login"
}).click();
```

---

# Handling Nested Components

```javascript
await page
.locator("dashboard")
.locator("user-profile")
.locator("button")
.click();
```

---

# How to Identify Shadow DOM in Browser

Open DevTools (F12).

Inspect the element.

If you see

```text
#shadow-root (open)
```

then Playwright can access it.

Example

```html
<custom-input>

#shadow-root (open)

<input>

</custom-input>
```

---

# Closed Shadow DOM

Example

```text
#shadow-root (closed)
```

Playwright cannot directly locate elements inside a closed Shadow DOM.

---

# Can Playwright Access Closed Shadow DOM?

❌ No.

Reason:

The browser itself blocks access to closed shadow roots.

Possible workarounds depend on the application, such as exposing test IDs or asking developers to use an open shadow root in test environments.

---

# Advantages

- Automatic support for open Shadow DOM
- Cleaner code
- No context switching
- Supports all locator strategies
- Works with nested shadow roots

---

# Limitations

- Cannot access closed Shadow DOM directly
- Depends on browser restrictions
- Closed components may require application changes for testing

---

# Best Practices

✅ Prefer user-facing locators.

```javascript
page.getByRole()
```

---

✅ Use

```javascript
getByLabel()
```

whenever possible.

---

✅ Prefer

```javascript
getByPlaceholder()
```

over CSS selectors.

---

✅ Keep locator chains short.

---

✅ Verify whether the shadow root is open or closed before writing locators.

---

# Common Mistakes

❌ Assuming every component uses Shadow DOM.

---

❌ Trying to access closed Shadow DOM.

---

❌ Writing unnecessarily long CSS selectors.

---

❌ Ignoring accessibility locators.

---

# Playwright vs Selenium

| Feature | Playwright | Selenium |
|----------|------------|-----------|
| Open Shadow DOM | ✅ Automatic | ❌ Requires `getShadowRoot()` or JavaScript (depending on language/binding) |
| Closed Shadow DOM | ❌ No | ❌ No |
| Nested Shadow DOM | ✅ Automatic | ⚠️ Manual handling required |
| getByRole() Support | ✅ Yes | ❌ No built-in equivalent |
| getByLabel() Support | ✅ Yes | ❌ No built-in equivalent |

---

# Interview Questions

### Q1 What is Shadow DOM?

Shadow DOM is an encapsulated DOM tree attached to an element to isolate its structure and styles from the main document.

---

### Q2 Why is Shadow DOM used?

To create reusable, isolated UI components without style or script conflicts.

---

### Q3 What are the two types of Shadow DOM?

- Open Shadow DOM
- Closed Shadow DOM

---

### Q4 Can Playwright access Shadow DOM?

Yes, Playwright automatically works with **open** Shadow DOM.

---

### Q5 Can Playwright access Closed Shadow DOM?

No.

Closed Shadow DOM is protected by the browser and cannot be directly accessed.

---

### Q6 What is a Shadow Host?

The HTML element that contains the Shadow Root.

---

### Q7 What is a Shadow Root?

The root node of the Shadow DOM tree.

---

### Q8 How do you identify Shadow DOM in DevTools?

Inspect the element. If you see:

```text
#shadow-root (open)
```

it is an open Shadow DOM.

---

# Summary

- Shadow DOM isolates HTML, CSS, and JavaScript inside web components.
- Playwright automatically supports **open Shadow DOM**.
- Closed Shadow DOM cannot be accessed directly.
- Prefer accessibility-based locators (`getByRole`, `getByLabel`, etc.) whenever possible.
- Keep locator chains readable and maintainable.
