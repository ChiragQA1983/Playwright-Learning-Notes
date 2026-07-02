# 📋 Playwright Actions - Select Option

## 📌 Select Option Action

The `selectOption()` method is used to **select one or more options from an HTML `<select>` dropdown**. It allows you to select options using their **value**, **label (visible text)**, or **index**.

Playwright automatically waits for the dropdown to become visible, enabled, and ready for interaction before selecting the option.

> **Note:** `selectOption()` works only with native HTML `<select>` elements. It does **not** work with custom dropdowns (e.g., Bootstrap, Material UI, React Select, Ant Design).

---

# Syntax

```javascript
await page.locator('locator').selectOption('value');
```

or

```javascript
await page.selectOption('locator', 'value');
```

> ✅ **Recommended:** Use `locator().selectOption()` because it is more reliable, reusable, and supports Playwright's auto-waiting mechanism.

---

# Example HTML

```html
<select id="country">

    <option value="in">India</option>

    <option value="us">United States</option>

    <option value="uk">United Kingdom</option>

</select>
```

---

# Example 1: Select by Value

```javascript
import { test } from '@playwright/test';

test('Select Country by Value', async ({ page }) => {

    await page.goto('https://example.com');

    await page.locator('#country').selectOption('in');

});
```

---

# Example 2: Select by Label (Visible Text)

```javascript
await page.locator('#country').selectOption({

    label: 'India'

});
```

---

# Example 3: Select by Index

```javascript
await page.locator('#country').selectOption({

    index: 1

});
```

> The index starts from **0**.

---

# Example 4: Select Using Different Locators

### By ID

```javascript
await page.locator('#country').selectOption('in');
```

### By Label

```javascript
await page.getByLabel('Country').selectOption('in');
```

### By CSS Selector

```javascript
await page.locator('select[name="country"]').selectOption('in');
```

---

# Example 5: Select Multiple Options

For a dropdown that supports multiple selection (`multiple` attribute):

```javascript
await page.locator('#languages').selectOption([
    'java',
    'python',
    'javascript'
]);
```

---

# Example 6: Select Multiple Options by Label

```javascript
await page.locator('#languages').selectOption([
    { label: 'Java' },
    { label: 'Python' }
]);
```

---

# Example 7: Remove All Selected Options

For a multiple-select dropdown:

```javascript
await page.locator('#languages').selectOption([]);
```

---

# Verify Selected Option

```javascript
await page.locator('#country').selectOption('in');

await expect(
    page.locator('#country')
).toHaveValue('in');
```

---

# Get Selected Value

```javascript
const selectedValue = await page.locator('#country').inputValue();

console.log(selectedValue);
```

---

# Select Option Using an Object

```javascript
await page.locator('#country').selectOption({

    value: 'in'

});
```

```javascript
await page.locator('#country').selectOption({

    label: 'India'

});
```

```javascript
await page.locator('#country').selectOption({

    index: 0

});
```

---

# Difference Between Native and Custom Dropdowns

| Native Dropdown | Custom Dropdown |
|-----------------|-----------------|
| Uses `<select>` tag | Uses `<div>`, `<span>`, `<ul>`, etc. |
| Supports `selectOption()` | Does not support `selectOption()` |
| Browser-controlled | Application-controlled |
| Easy to automate | Usually requires `click()` actions |

---

# Handling Custom Dropdowns

For custom dropdowns, use click actions.

```javascript
await page.locator('#countryDropdown').click();

await page.getByText('India').click();
```

---

# Best Practices

✅ Use `selectOption()` only for native HTML `<select>` elements.

✅ Prefer `locator.selectOption()` over `page.selectOption()`.

✅ Use selection by **value** whenever possible because it is less likely to change than visible text.

✅ Verify the selected option using `toHaveValue()`.

✅ Use `click()` for custom dropdowns.

---

# Common Interview Questions

### Q1. What is the purpose of `selectOption()`?

**Answer:**

The `selectOption()` method selects one or more options from a native HTML `<select>` dropdown.

---

### Q2. Can `selectOption()` be used with custom dropdowns?

**Answer:**

No. It works only with native HTML `<select>` elements. Custom dropdowns require `click()` and locator-based interactions.

---

### Q3. How can you select an option by visible text?

**Answer:**

```javascript
await page.locator('#country').selectOption({

    label: 'India'

});
```

---

### Q4. How do you verify the selected option?

**Answer:**

```javascript
await expect(
    page.locator('#country')
).toHaveValue('in');
```

---

### Q5. How do you select multiple options?

**Answer:**

```javascript
await page.locator('#languages').selectOption([
    'java',
    'python'
]);
```

---

# Summary

| Method | Purpose |
|--------|---------|
| `selectOption('value')` | Select by value |
| `selectOption({ label })` | Select by visible text |
| `selectOption({ index })` | Select by index |
| `selectOption([])` | Clear all selected options (multiple-select) |
| `toHaveValue()` | Verify selected value |
| `inputValue()` | Get the selected value |

---

# Key Points

- `selectOption()` is used only with native HTML `<select>` dropdowns.
- You can select options by **value**, **label**, or **index**.
- Multiple options can be selected if the dropdown supports the `multiple` attribute.
- Use `toHaveValue()` to verify the selected option.
- For custom dropdowns (Bootstrap, React, Material UI, Ant Design, etc.), use `click()` actions instead of `selectOption()`.
