# 📤 Playwright Actions - Upload File

## 📌 Upload File Action

The `setInputFiles()` method is used to **upload one or more files** to a web application. It works with HTML `<input type="file">` elements by assigning the specified file(s) to the input field.

Unlike Selenium, Playwright **does not interact with the operating system's file chooser**. Instead, it uploads files directly to the file input, making file uploads faster and more reliable.

Playwright automatically waits for the file input element to become visible, enabled, and ready before uploading the file.

---

# Syntax

```javascript
await page.locator('locator').setInputFiles('filePath');
```

or

```javascript
await page.setInputFiles('locator', 'filePath');
```

> ✅ **Recommended:** Use `locator().setInputFiles()` because it is more reliable, reusable, and supports Playwright's auto-waiting mechanism.

---

# Example HTML

```html
<input type="file" id="uploadFile">
```

---

# Example 1: Upload a Single File

```javascript
import { test } from '@playwright/test';

test('Upload Single File', async ({ page }) => {

    await page.goto('https://example.com');

    await page.locator('#uploadFile')
        .setInputFiles('test-data/sample.pdf');

});
```

---

# Example 2: Upload Multiple Files

```javascript
await page.locator('#uploadFile')
    .setInputFiles([
        'test-data/file1.pdf',
        'test-data/file2.pdf',
        'test-data/file3.pdf'
    ]);
```

> The input element must support multiple file uploads (`multiple` attribute).

---

# Example 3: Upload Using Different Locators

### By ID

```javascript
await page.locator('#uploadFile')
    .setInputFiles('test-data/sample.pdf');
```

### By Label

```javascript
await page.getByLabel('Upload File')
    .setInputFiles('test-data/sample.pdf');
```

### By CSS Selector

```javascript
await page.locator('input[type="file"]')
    .setInputFiles('test-data/sample.pdf');
```

---

# Example 4: Upload Using Relative Path

```javascript
await page.locator('#uploadFile')
    .setInputFiles('./uploads/image.png');
```

---

# Example 5: Upload Using Absolute Path

```javascript
await page.locator('#uploadFile')
    .setInputFiles('C:/Users/Admin/Documents/sample.pdf');
```

> Relative paths are recommended because they make your tests portable across different environments.

---

# Example 6: Upload a File from Memory

You can upload a file without creating it on disk.

```javascript
await page.locator('#uploadFile')
    .setInputFiles({

        name: 'sample.txt',

        mimeType: 'text/plain',

        buffer: Buffer.from('Hello Playwright')

    });
```

---

# Example 7: Remove Uploaded File

Pass an empty array to clear the selected file(s).

```javascript
await page.locator('#uploadFile')
    .setInputFiles([]);
```

---

# Handle File Chooser

Some applications open the file chooser after clicking an upload button.

```javascript
const fileChooserPromise =
    page.waitForEvent('filechooser');

await page.locator('#uploadButton').click();

const fileChooser =
    await fileChooserPromise;

await fileChooser.setFiles(
    'test-data/sample.pdf'
);
```

> Use this approach only when the application opens a file chooser dynamically.

---

# Verify File Upload

```javascript
await page.locator('#uploadFile')
    .setInputFiles('test-data/sample.pdf');

await expect(
    page.locator('#fileName')
).toContainText('sample.pdf');
```

---

# Wait Before Uploading

Playwright automatically waits until the file input is:

- Visible
- Enabled
- Ready for interaction

```javascript
await page.locator('#uploadFile')
    .setInputFiles('test-data/sample.pdf');
```

No explicit wait is required in most cases.

---

# Difference Between `setInputFiles()` and File Chooser

| Feature | `setInputFiles()` | File Chooser |
|----------|-------------------|--------------|
| Uploads directly | ✅ Yes | ❌ No |
| Uses file input | ✅ Yes | ✅ Yes |
| Requires `waitForEvent()` | ❌ No | ✅ Yes |
| Recommended | ✅ Yes | ⚠️ Only when needed |

---

# Real-Time Use Cases

### Upload Profile Picture

```javascript
await page.locator('#profileImage')
    .setInputFiles('uploads/profile.png');
```

---

### Upload Resume

```javascript
await page.locator('#resume')
    .setInputFiles('documents/resume.pdf');
```

---

### Upload Multiple Documents

```javascript
await page.locator('#documents')
    .setInputFiles([
        'docs/id.pdf',
        'docs/address.pdf'
    ]);
```

---

# Best Practices

✅ Prefer `locator.setInputFiles()` over `page.setInputFiles()`.

✅ Use relative file paths whenever possible.

✅ Verify that the upload was successful using assertions.

✅ Use `waitForEvent('filechooser')` only when the application opens a file chooser dynamically.

✅ Avoid `waitForTimeout()` before uploading files.

---

# Common Interview Questions

### Q1. What is the purpose of `setInputFiles()`?

**Answer:**

`setInputFiles()` uploads one or more files to an HTML file input element.

---

### Q2. Can Playwright upload multiple files?

**Answer:**

Yes, provided the file input supports multiple file selection.

```javascript
await page.locator('#uploadFile')
    .setInputFiles([
        'file1.pdf',
        'file2.pdf'
    ]);
```

---

### Q3. How do you remove an uploaded file?

**Answer:**

```javascript
await page.locator('#uploadFile')
    .setInputFiles([]);
```

---

### Q4. When should you use `waitForEvent('filechooser')`?

**Answer:**

Use it when clicking a button opens the browser's file chooser dialog before selecting a file.

---

### Q5. Which approach is recommended?

**Answer:**

`locator.setInputFiles()` is the recommended approach because it is simpler, more reliable, and leverages Playwright's built-in auto-waiting.

---

# Summary

| Method | Purpose |
|--------|---------|
| `setInputFiles('file')` | Upload a single file |
| `setInputFiles([])` | Remove uploaded file(s) |
| `setInputFiles(['file1','file2'])` | Upload multiple files |
| `waitForEvent('filechooser')` | Handle a dynamic file chooser |
| `fileChooser.setFiles()` | Select files using the file chooser |

---

# Key Points

- `setInputFiles()` is Playwright's built-in method for uploading files.
- It works only with HTML `<input type="file">` elements.
- You can upload a single file, multiple files, or even an in-memory file.
- Use relative file paths to make tests portable.
- Prefer `locator.setInputFiles()` over `page.setInputFiles()` for better readability and maintainability.
