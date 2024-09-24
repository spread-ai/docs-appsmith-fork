---
title: Creating a Studio application
description: A guide on creating an application in Studio, that uses your product knowledge.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

Studio allows you to visualize, manage, and interact with the product knowledge [imported](../data-import/data-import-overview.md) into the SPREAD platform. With Studio you can supplement the Core Applications from SPREAD, such as [Connectivity Analyzer](../../applications/using-connectivity-analyzer/connectivity-analyzer-overview.md) and [Circuit Diagram Creator](../../applications/using-circuit-diagram-creator/circuit-diagram-creator-overview.md), with custom applications to suit your needs. The Studio canvas offers a low-code visual environment to create application screens and can be integrated with [Flows](../using-flows/using-flows-overview.md) to further refine and transform the data you use in the application.

## Organizing workspaces

Studio is organized into workspaces, where the applications you create are organized. You can use workspaces to segment applications by type, development stage, or any organizational pattern that works for your use case. To add workspaces select the `+` icon in the workspaces window.

=== "Create a new application"

	To import an application, select **Create New** > **New app**.

=== "Add users to workspaces"

	To add users to a Workspace, select the **Share** button. Or you can select **・・・** > **Settings** > **Add users**. For more on the permissions available for users, see [Default roles](../../platform/user-management/user-management-and-permissions.md#default-roles).

=== "Import an application"

	To import an application, select **Create New** > **Import**.

=== "Change workspace settings"

	To change the Workplace settings, select **・・・** > **Settings** > **General Settings**.

<figure markdown="span">
	![Adding a workspace in Studio](src/adding-workspaces-to-studio.png)
	<figcaption>Adding a workspace in Studio</figcaption>
</figure>

!!! info "Avoid overwriting production applications"

    We strongly recommend that you keep your production applications separate from applications in development by moving them to a separate Workspace. This puts an extra barrier to any unintentional changes to production applications.

## Navigating the Studio canvas

The Studio canvas is where you create your application. The canvas is divided into the following areas:

1 - **Top bar:** Here you can change the name of the application, preview your application, and publish your application to the launcher.<br>
2 - **Explorer window:** Configure the data sources you want to use and pick widgets to add to the canvas.<br>
3 - **Properties window:** Configure widget or canvas properties.<br>
4 - **Bottom bar:** Deploy your application to Git and access documentation.<br>
5 - **Canvas area:** The screen that's displayed to application users, where you can drag-and-drop widgets.<br>

<figure markdown="span">
	![Navigating the SPREAD Studio canvas](src/navigating-spread-studio-canvas.png)
	<figcaption>Navigating the SPREAD Studio canvas</figcaption>
</figure>

## Creating your application

Applications fall into two types: ones that read data flows from a data source and display it using widgets and ones that write data flows by capturing data from widgets and then validating the data before sending it to a data source. To start creating an application its useful to think of what data flow you're working with, what the interface should look like, and how the user's interaction with the application plays out. Once you have these parameters you can start building out the app.

---

To create multi-page applications go to the **Pages** section underneath the app title and select **+**. Interactions between pages will need to be built into each page.

---

### Configure the application

Select the gear icon in the bottom-right corner to open **App Settings**. Here you can set the name of your application, the styling of your application, and change the canvas view.

<figure markdown="span">
	![Styling your Studio application](src/styling-studio-applications.png)
	<figcaption>Styling your Studio application</figcaption>
</figure>

In the **Theme** submenu in the App settings, you can configure font, primary color, background color, border, and shadow. To configure the canvas size use the **Properties** panel on the right-hand side.

### Connect data sources

To set data sources select **Data** in the left-hand side panel. This opens a settings window to connect your data from API services, integrations, or databases. You can save queries and mutations done in API services to use later in the logic of your application.

For more on connecting data sources, see [AppSmith Datasources](https://docs.appsmith.com/connect-data/reference). Please be aware that not all data sources in AppSmith are supported by SPREAD Studio.

### Build the UI


In the **Editor** view (from the options in the left-hand side panel) you can drag and drop widgets from the **Widgets** tab to start building your user interface. Widgets are resizable and can be moved around the canvas. Each widget opens a property window in right-hand side of the screen, where you to set details for that widget and style it individually.

For example, the **DatePicker** widget has options for setting the date format, the default date, the label position and text, and other settings associated with dates. The **Style** tab is where you can set font, color, and border options. You can delete or copy a widget by selecting the icons at the top of the properties window.

Certain widgets allow you to use variables for their settings. In Studio, variables are enclosed by double curly braces. For example: `{{ '{{ app1.myVariable }}' }}`. For more on widgets and their options, see the [Widget Reference](reference/studio-widget-reference.md).

### Write the logic

Certain widgets allow you to use variables for their settings. In Studio, variables are enclosed by double curly braces. For example: `{{ "{{ app1.myVariable }}" }}`. For more on widgets and their options, see the [Widget Reference](reference/studio-widget-reference.md).

The logic of your application determines what happens when the user enters data, clicks on a button, or performs any action in your application. In many cases the logic will be attached to events that the user may perform on a widget. For example, an **onClick** event for a button could trigger a JavaScript function, execute a query, or change the contents of the screen.

<figure markdown="span">
	![The contextual menu for the onClick event in SPREAD Studio](src/onclick-event-studio.png)
	<figcaption>The contextual menu for the onClick event in SPREAD Studio</figcaption>
</figure>

JavaScript code is enclosed with double curly braces. For example: `{{ '{{ SelectWidgetName.selectedOptionValue === "1" ? "Option 1" : "Option 2" }}' }}`. Global objects, such as the [AppSmith object](https://docs.appsmith.com/reference/appsmith-framework/context-object), and Global Functions, such as [storeValue](https://docs.appsmith.com/reference/appsmith-framework/widget-actions/store-value), are available to use in your code.

!!! info "More Global Objects and Global Functions"

    For a complete reference of the Global Objects available in Studio, see the [AppSmith documentation on Global Objects](https://docs.appsmith.com/write-code/reference). Likewise for Global Functions, see the [AppSmith documentation on Global Functions](https://docs.appsmith.com/reference/appsmith-framework/widget-actions).

For complex implementations, you can install additional JavaScript libraries by selecting the Box icon in the bottom-left corner. The default libraries are [lodash.js](https://lodash.com/) for modularity and performance, [moment.js](https://momentjs.com/) for date and time handling, and [forge.js](https://github.com/digitalbazaar/forge) for managing cryptographic tools.

<figure markdown="span">
	![Adding JavaScript libraries in SPREAD Studio](src/adding-javascript-libraries-in-studio.png)
	<figcaption>Adding JavaScript libraries in SPREAD Studio</figcaption>
</figure>


### Preview, publish, and deploy to Git

Once your application is complete, you can preview it by selecting the Play icon in the top bar. Select the icon again to return to edit mode.

!!! info "Debugging your application"

    If there are errors in your application a notification will appear in the bottom bar. Selecting the notification opens an application inspector with tabs for logging, inspecting entities, and seeing errors.
    ![The debug console in Studio](src/debugging-errors-in-studio.png)

If everything works as it should you can publish your application by selecting the **Publish** button the top-right corner. Once published, your new application will appear on the Launcher page as a tile. We recommend using version control by selecting **Connect Git** in the bottom bar and following the instructions in the modals to connect send your changes to a remote repo on GitHub, GitLab, or Bitbucket.
