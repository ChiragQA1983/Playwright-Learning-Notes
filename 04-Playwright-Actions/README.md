# 🎬 Playwright Actions

## 📖 Overview

After locating an element, the next step in Playwright automation is to **perform actions** on it.

Playwright provides built-in methods to interact with web elements such as clicking buttons, entering text, selecting dropdown values, uploading files, hovering over elements, dragging items, pressing keyboard keys, and much more.

Unlike many other automation frameworks, Playwright automatically waits for elements to become actionable before performing an action, making tests more reliable and reducing flaky failures.

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Perform mouse actions
- Perform keyboard actions
- Interact with form elements
- Handle dropdowns
- Upload and download files
- Perform drag-and-drop
- Scroll elements into view
- Dispatch browser events
- Execute JavaScript on page elements
- Apply Playwright action best practices

---

# 📚 Topics Covered

## Mouse Actions

- click()
- dblclick()
- hover()
- dragTo()

---

## Keyboard Actions

- fill()
- press()
- type()
- pressSequentially()
- focus()
- blur()

---

## Form Actions

- check()
- uncheck()
- selectOption()
- setChecked()

---

## File Handling

- setInputFiles()

---

## Scrolling

- scrollIntoViewIfNeeded()

---

## Browser Events

- dispatchEvent()

---

## JavaScript Execution

- evaluate()
- evaluateAll()

---

## Advanced Actions

- Locator Chaining
- Multiple Element Actions
- Working with Dynamic Elements

---

# 📂 Folder Structure

```text
04-Playwright-Actions
│
├── README.md
├── 01-click().md
├── 02-dblclick().md
├── 03-hover().md
├── 04-fill().md
├── 05-clear().md
├── 06-press().md
├── 07-check().md
├── 08-uncheck().md
├── 09-selectOption().md
├── 10-focus().md
├── 11-blur().md
├── 12-scrollIntoViewIfNeeded().md
├── 13-setInputFiles().md
├── 14-dragTo().md
├── 15-dispatchEvent().md
├── 16-evaluate().md
├── 17-evaluateAll().md
├── 18-Best-Practices.md
├── 19-Interview-Questions.md
└── 20-Real-Project-Examples.md
```

---

# 📌 Playwright Action Categories

| Category | Description |
|-----------|-------------|
| Mouse | Click, Double Click, Hover, Drag & Drop |
| Keyboard | Fill, Press, Type, Focus |
| Form | Checkbox, Radio Button, Dropdown |
| File | Upload Files |
| Scroll | Scroll into View |
| JavaScript | Execute JavaScript |
| Browser Events | Dispatch Events |

---

# 🚀 Why Playwright Actions?

Playwright automatically performs **actionability checks** before interacting with an element.

Before performing an action, Playwright verifies that the element is:

- Attached to the DOM
- Visible
- Stable (not animating)
- Enabled
- Able to receive pointer events

These built-in checks reduce flaky tests and eliminate many explicit waits.

---

# 💡 Best Practices

- Prefer accessibility locators (`getByRole`, `getByLabel`, etc.) before performing actions.
- Avoid unnecessary `waitForTimeout()` calls.
- Let Playwright's auto-waiting work for you.
- Use locator chaining to keep code readable.
- Prefer `fill()` over repeated key presses when entering text.
- Use meaningful assertions after actions to verify expected behavior.

---

# 🎤 Interview Questions

- What are Playwright Actions?
- What is Actionability in Playwright?
- Difference between `click()` and `dblclick()`?
- Difference between `fill()` and `type()`?
- When should `hover()` be used?
- How do you upload files in Playwright?
- How does Playwright reduce flaky tests during actions?
- What checks does Playwright perform before clicking an element?

---

# 📌 Summary

Actions are one of the core features of Playwright. They allow you to interact with web elements in a reliable way while benefiting from 
Playwright's automatic waiting and actionability checks. Understanding these methods is essential for building stable, maintainable automation tests.
