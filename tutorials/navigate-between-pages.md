---
title: How to navigate between pages in Studio
description: Learn how to navigate between pages in Studio.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

Studio provides the [navigateTo](../reference/framework/global-functions.md#navigateTo) function that lets you navigate between pages within your app. This guide shows you how to implement page navigation.

## Prerequisite knowledge

- [x] Basic understanding of how to [build Studio applications](../creating-studio-applications.md).
- [x] Access to a SPREAD Studio environment.

## Instructions

You can use a [Text](../reference/widgets/text.md) widget or an [Icon Button](../reference/widgets/icon-button.md) to navigate between pages.

### 1. Add the widget

Drop an Icon button widget and set it's **onClick** property to navigate to another page. You can do this in the following ways:

- Using the **Navigate to** action and entering the page name or a URL to navigate to. This action tells the app where to navigate when the Icon is clicked.
- Using the **JS** button and using the following code to navigate to a page within the app where `page_name` is the name of the target page:

```js
{{ '{{navigateTo("page_name")}}' }}
```

To navigate to an external URL, pass a full URL instead of a page name.

```js
navigateTo('https://www.example.com') // (1)!
```

1. Remember to enclose this in mustache syntax.

### 2. Open link in new window or tab

To open the linked page in a new browser tab or window, use the third parameter.

```js
navigateTo('page_name', { }, 'NEW_WINDOW') // (1)!
```

1. Remember to enclose this in mustache syntax.