---
title: Create a custom navigation bar
description: Learn how to create a custom navigation bar in Studio.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

You can customize and group menu options with a custom navigation bar. This page shows you steps to create a custom navigation bar.

## Prerequisite knowledge

- [x] Basic understanding of how to [build Studio applications](../creating-studio-applications.md).
- [x] Access to a SPREAD Studio environment.

## Instructions

To create a custom navigation bar, follow these steps:

1. Create all the pages in the application you would like to display in the custom navigation bar.
2. You can create a custom navigation bar using [Buttons](../reference/widgets/buttons.md), [Menu Buttons](../reference/widgets/menu-items.md), or [Button Groups](../reference/widgets/button-groups.md). On the first page of your app, add a Button Group widget to hold the menu items for the navigation bar. To rearrange and configure the buttons, click the gear icon **⚙**️ beside each button. You can later export the components of the navigation bar and use it in the rest of your application's pages.
3. To configure the nested menu for the nav bar, click the gear icon **⚙**️ beside the Menu button of the Button Group.
4. Add the **Navigate to** action to each button's **OnClick** event to navigate to the desired page. To add action to the **onClick** event of the Menu items, click the gear icon **⚙**️ beside the menu item.
5. To export the navigation bar, click the menu icon (three dots) beside the page. Select **Export** and click the widgets you want to export.
6. Click **Export selected entities**. The system downloads a JSON file containing the chosen widget details.
7. Go to the page where you want to import the navigation bar and select the Menu icon (three dots) beside the page. Select **Import**, and then select the downloaded JSON file. Your page now includes the navigation bar.
