getByTitle

Allows locating elements by their title attribute.

Usage

Consider the following DOM structure.

<span title='Issues count'>25 issues</span>

You can check the issues count after locating it by the title text:

await expect(page.getByTitle('Issues count')).toHaveText('25 issues');

Arguments

text string | RegExp#

Text to locate the element for.

options Object (optional)

exact boolean (optional)#

Whether to find an exact match: case-sensitive and whole-string. Default to false. Ignored when locating by a regular expression. Note that exact match still trims whitespace.

Returns

Locator#
