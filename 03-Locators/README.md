# 🎯 Playwright Locators

## What is a Locator?

A locator is used to identify and interact with web elements on a page. Playwright provides powerful built-in locator strategies that make automation scripts more stable and reliable.

---

## Why are Locators Important?

- Identify web elements accurately
- Improve test stability
- Reduce flaky tests
- Support auto-waiting
- Make scripts easier to maintain

---

## Topics Covered

- What is a Locator?
- locator()
- getByRole()
- getByText()
- getByLabel()
- getByPlaceholder()
- getByAltText()
- getByTitle()
- getByTestId()
- CSS Selector
- XPath
- Chaining Locators
- Filter Locators
- Best Practices
- Common Mistakes


---

## Example

```javascript
await page.getByRole('button', { name: 'Login' }).click();
```

---

## Learning Goal

By the end of this chapter, you will be able to choose the best locator strategy for different web elements.
