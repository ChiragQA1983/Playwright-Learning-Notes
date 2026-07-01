FrameLocator represents a view to the iframe on the page. It captures the logic sufficient to retrieve the iframe and locate elements in that iframe. 
FrameLocator can be created with either locator.contentFrame(), page.frameLocator() or locator.frameLocator() method.

const locator = page.locator('#my-frame').contentFrame().getByText('Submit');
await locator.click();


Strictness

Frame locators are strict. This means that all operations on frame locators will throw if more than one element matches a given selector.

// Throws if there are several frames in DOM:
await page.locator('.result-frame').contentFrame().getByRole('button').click();

// Works because we explicitly tell locator to pick the first frame:
await page.locator('.result-frame').contentFrame().first().getByRole('button').click();


Converting Locator to FrameLocator

If you have a Locator object pointing to an iframe it can be converted to FrameLocator using locator.contentFrame().

Converting FrameLocator to Locator

If you have a FrameLocator object it can be converted to Locator pointing to the same iframe using frameLocator.owner().

Methods
frameLocator
Added in: v1.17 
When working with iframes, you can create a frame locator that will enter the iframe and allow selecting elements in that iframe.

Usage

frameLocator.frameLocator(selector);

Arguments

selector string#

A selector to use when resolving DOM element.

Returns

FrameLocator#
