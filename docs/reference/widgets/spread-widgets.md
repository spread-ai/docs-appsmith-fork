---
title: SPREAD widget Reference
description: A reference of the widgets available to use when creating your Studio application.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This reference documents SPREAD widgets that are built into Studio. In the reference below:

* **Content** properties denote the content properties you can set in the widget.
* **Event** properties denote the events that you can attach actions and logic to.
* **Style** properties denote the styling that you can set for the widget.
* **Reference** properties return the values of a widget property.
* **Methods** modify the values of widget properties at runtime using JavaScript [promises](../../writing-code-in-studio/using-js-promises.md).

### Badge

The badge widget is a visual element to highlight important information or status updates. The badge widget is used to indicate new or unread messages, notifications, statuses, or other important information.

<figure markdown="span">
	![The Badge widget in SPREAD Studio](../src/badge-widget-on-spread-studio.png)
	<figcaption>The Badge widget in SPREAD Studio</figcaption>
</figure>

### Widget properties

| Property Type | Name | Type | Description |
| --- | --- | --- | --- |
| Content | Label | string | Sets the text that appears on the badge. |
| Content | Visible | boolean | Controls the visibility of the widget. |
| Content | Height | | Set how the badge height behaves. Options are `Auto Height`, `Auto Height withy limits`, and `Fixed`. The height can be set in the canvas by resizing the widget. |
| Events | onClick | | Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when the badge is clicked. You can chain multiple actions together, and all the nested actions would run simultaneously. |
| Style | Color | | Sets the background color of the badge. Available values together with their respective CSS color value:<br> * Neutral (#d4d4d8)<br> * Danger (#fca5a5)<br>* Warning (#fcd34d)<br>* Success (#6ee7b7)<br> * Custom (allows you to input a custom value). |
| Reference | `label` | string | Returns the value of the badge's label property. |
| Reference | `isVisible` | boolean | Indicates the visibility state of a widget, with true indicating it is visible and false indicating it is hidden. |
| Methods | `setColor (param: string): Promise`​ | | Sets the background color of the badge. Expects a CSS color value. |
| Methods | `setLabel (param: string): Promise`​ | | Sets the label of the badge. |
| Methods | `setVisibility (param: boolean): Promise`​ | | Sets the visibility of the widget. |

### Graph

The graph widget is a visual element to create node diagrams.

<figure markdown="span">
	![The Graph widget in SPREAD Studio](../src/graph-widget-on-spread-studio.png){height="250px"}
	<figcaption>The Graph widget in SPREAD Studio</figcaption>
</figure>

### Widget properties

| Property Type | Name | Type | Description |
| --- | --- | --- | --- |
| Content | Edges | object | Defines edges of graph. |
| Content | Nodes | object | Defines nodes of graph. |
| Content | Selected nodes | array  | Defines selected nodes indices of graph. |
| Content | Hidden node ids | array  | Defines nodes that are hidden in the graph. |
| Events | onSelectionChange | | Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when the selection is changed. You can chain multiple actions together, and all the nested actions would run simultaneously. |
| Events | onRightChange | | Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when the right-click mouse action is used. You can chain multiple actions together, and all the nested actions would run simultaneously. |
| Style | Node figure | | Sets the shape of nodes. Can be `Rounded rectangle` or `circle`. |
| Style | Toolbar | boolean | Hide or show the toolbar, which has zoom and focus options. |
| Style | Mode | | Sets the type of node diagram. Can be `Force directed` or `Hierarchical`. Hierarchical has options for direction. |
| Style | Size | integer | Sets the size of the node diameter, node text size, node border size, and the selected node border size. |
| Style | Color |  | Sets the color of the background, node text, node color, node border, edge, selected node background, and selected node border. |

### Guided Event Chain

The Guided Event Chain widget is a visual element to display the flow of guided events.

<figure markdown="span">
	![The Guided Event Chain widget in SPREAD Studio](../src/guided-event-chain-widget-on-spread-studio.png){height="250px"}
	<figcaption>The Guided Event Chain widget in SPREAD Studio</figcaption>
</figure>

### Widget properties

| Property Type | Name | Type | Description |
| --- | --- | --- | --- |
| Content | Clusters | array | Defines clusters. |
| Content | Clusters Cards | array | Defines clusters cards. |
| Content | Links | array  | Defines links. |
| Events | onAddClusterClick | | Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when an add button on cluster is clicked. You can chain multiple actions together, and all the nested actions would run simultaneously. |
| Events | onEditOnCardClick | | Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when an edit button on card is clicked. You can chain multiple actions together, and all the nested actions would run simultaneously.  |
| Events | onAddOnCardClick | | Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when an add button on card is clicked. You can chain multiple actions together, and all the nested actions would run simultaneously.  |
| Events | onDeleteOnCardClick | | Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when a delete button on card is clicked. You can chain multiple actions together, and all the nested actions would run simultaneously.  |
| Events | onEditOnCardItemClick | | Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when an edit button on card item is clicked. You can chain multiple actions together, and all the nested actions would run simultaneously.  |
| Events | onDeleteOnCardItem | | Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when an delete button on card item is clicked. You can chain multiple actions together, and all the nested actions would run simultaneously.  |
| Content | Linked Filter Placeholder | string  | Placeholder for the linked filter on the cluster. |
| Content | Cluster Add Button Tooltip | string  | Tooltip for the add button on the cluster. |
| Content | Card Edit Button Tooltip | string  | Tooltip for the edit button on the card. |
| Content | Card Add Button Tooltip | string  | Tooltip for the add button on the card. |
| Content | Card Delete Button Tooltip | string  | Tooltip for the delete button on the card. |
| Content | Card Item Edit Button | string  | Tooltip for the edit button on the card item. |
| Content | Card Item Delete Button | string  | Tooltip for the delete button on the card item. |

### Legend

The Legend widget is designed to display a list of items with labels and optional icons. It allows users to visually interpret and manage a collection of entries with various properties such as color and icon. The orientation of the legend can be set to auto, horizontal, or vertical.

<figure markdown="span">
	![The Legend widget in SPREAD Studio](../src/legend-widget-on-spread-studio.png)
	<figcaption>The Legend widget in SPREAD Studio</figcaption>
</figure>

### Widget properties

| Property Type | Name | Type | Description |
| --- | --- | --- | --- |
| Content | Entries | array | Defines legend entries. |
| Content | Orientation | string | Defines the orientation of the legend. Options are `Auto`, `Horizontal`, and `Vertical`. |
| Content | Disabled entries ids | array | Defines disabled entries ids of the legend. |
| Events | onDisabledEntriesChange | | Function that will be fired on legend disabled entries change. |
| Style | Background color | string | Sets the background color of the legend. |
| Style | Border color | string | Sets the color of the border. |
| Style | Border width | number | Sets the width of the border in pixels. |
| Style | Border radius | string | Rounds the corners of the widget's outer border edge. |
| Style | Box shadow | string | Enables you to cast a drop shadow from the frame of the widget. |

### Precedence Graph

The Precedence Graph widget is a visual element that represents the precedence of items in a concurrent system.

<figure markdown="span">
	![The Precedence Graph widget in SPREAD Studio](../src/precedence-graph-on-spread-studio.png){heigh="250px"}
	<figcaption>The Precedence Graph widget in SPREAD Studio</figcaption>
</figure>

### Widget properties

| Property Type | Name | Type | Description |
| --- | --- | --- | --- |
| Content | Clusters | array | Defines clusters. |
| Content | Clusters Cards | array | Defines clusters cards. |
| Content | Links | array  | Defines links. |
| Events | onAddClusterClick | | Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when an add button on cluster is clicked. You can chain multiple actions together, and all the nested actions would run simultaneously. |
| Events | onEditOnCardClick | | Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when an edit button on card is clicked. You can chain multiple actions together, and all the nested actions would run simultaneously.  |
| Events | onAddOnCardClick | | Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when an add button on card is clicked. You can chain multiple actions together, and all the nested actions would run simultaneously.  |
| Events | onDeleteOnCardClick | | Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when a delete button on card is clicked. You can chain multiple actions together, and all the nested actions would run simultaneously.  |
| Events | onEditOnCardItemClick | | Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when an edit button on card item is clicked. You can chain multiple actions together, and all the nested actions would run simultaneously.  |
| Events | onDeleteOnCardItem | | Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when an delete button on card item is clicked. You can chain multiple actions together, and all the nested actions would run simultaneously.  |
| Content | Linked Filter Placeholder | string  | Placeholder for the linked filter on the cluster. |
| Content | Cluster Add Button Tooltip | string  | Tooltip for the add button on the cluster. |
| Content | Card Edit Button Tooltip | string  | Tooltip for the edit button on the card. |
| Content | Card Add Button Tooltip | string  | Tooltip for the add button on the card. |
| Content | Card Delete Button Tooltip | string  | Tooltip for the delete button on the card. |
| Content | Card Item Edit Button | string  | Tooltip for the edit button on the card item. |
| Content | Card Item Delete Button | string  | Tooltip for the delete button on the card item. |

### Renderer

The Renderer widget is a visual element that renders 3D objects.

<figure markdown="span">
	![The Renderer widget in SPREAD Studio](../src/renderer-widget-on-spread-studio.png)
	<figcaption>The Renderer Graph widget in SPREAD Studio</figcaption>
</figure>

### Widget properties

| Property Type | Name | Type | Description |
| --- | --- | --- | --- |
| Content | Model |  | Defines the URL to the model scene directory. |
| Events | onModelLoaded | | Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when the model is loaded. You can chain multiple actions together, and all the nested actions would run simultaneously. |
| Content | Selected nodes IDs | array | Defines default selected nodes and groups. Group IDs take precedence over node IDs. |
| Events | onSelectionChange | | Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when node selection changes. You can chain multiple actions together, and all the nested actions would run simultaneously. |
| Content | Hide nodes IDs | array | Defines default hidden nodes. |
| Content | Markers | array  | Defines a list of markers. |
| Content | Selected marker ID | string  | Defines selected marker ID. |
| Content | Pills | array  | Defines a list of pills. |
| Content | Visible | boolean | Controls the visibility of the widget. |
| Content | Show Context Menu | boolean | Controls the visibility of the context menu. |
| Content | Show only | boolean | Controls the visibility of the "Show only" in the context menu. |
| Content | Show all | boolean | Controls the visibility of the "Show all" in the context menu. |
| Content | Hide | boolean | Controls the visibility of the "Hide" in the context menu. |
| Content | Active Collection ID | string | Specifies the active collection. Only when a collection is active so that its groups and nodes can be selected.  |
| Content | Collections | string | Defines collections, which encompass both node groups and individual nodes. When selecting nodes in the renderer, nodes within a group are treated as a single entity. Collection and group IDs must adhere to the hyphenated UUID format.  |
| Style | Toolbar | boolean | Hide or show the toolbar, which has zoom and focus options. |
| Style | Navigation cube | boolean | Hide or show the navigation cube, which has zoom and focus options. |
| Style | Ghosted Mode | boolean | Defines whether the entire model should be ghosted. When false, asks for node IDs. |
| Style | Selected marker shape color | hex  | Sets the color of the selected marker shape. |
| Style | Selected marker digit color | hex  | Sets the color of the selected marker digit. |
| Style | Size | integer | Sets the size of the node diameter, node text size, node border size, and the selected node border size. |
| Style | Selected marker scale | integer  | Changes the scale of the selected marker. |
| Style | Unselected marker shape color | hex  | Sets the color of the unselected marker shape. |
| Style | Unselected marker digit color | hex  | Sets the color of the unselected marker digit. |
| Style | Unselected marker scale | integer  | Changes the scale of the unselected marker. |

### Stepper

The Stepper widget displays a step-by-step process or workflow. It visually guides users through a sequence of tasks or stages in a concise, ordered manner. Stepper is implemented as a horizontal list of steps, with each step indicating the current, completed, or upcoming stage in the process.

<figure markdown="span">
	![The Stepper widget in SPREAD Studio](../src/stepper-widget-on-spread-studio.png)
	<figcaption>The Stepper widget in SPREAD Studio</figcaption>
</figure>

### Widget properties

| Property Type | Name | Type | Description |
| --- | --- | --- | --- |
| Content | Steps |  | The defined steps in the process. |
| Content | Default step |  | The specified default step. |
| Content | Visible | boolean | Controls the visibility of the widget. |
| Content | Show steps | boolean | Hides the steps so that different widgets can be displayed based on the default step. |
| Content | Height | | Set how the badge height behaves. Options are `Auto Height`, `Auto Height withy limits`, and `Fixed`. The height can be set in the canvas by resizing the widget. |
| Events | onStepSelected | | Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed on the selected step change. You can chain multiple actions together, and all the nested actions would run simultaneously. |
| Style | Border color |  | Sets the color of the border. |
| Style | Border width | integer | Sets the width of the border. |
| Style | Border radius | | Rounds the corners of the icon buttons. |
| Style | Box shadow |  | Enables you to cast a drop shadow from the frame of the widget. |

### Topology Viewer

The Topology Viewer widget displays the graph with nodes and edges oriented as a tree. It helps visualize the communication between nodes (for example, components exchanging signals) and any other type of topology.

<figure markdown="span">
	![The Topology Viewer widget in SPREAD Studio](../src/topology-viewer-widget-on-spread-studio.png)
	<figcaption>The Topology Viewer widget in SPREAD Studio</figcaption>
</figure>

### Supported features

* Auto layout and ability to drag the nodes to the desired location, with no permanent coordinates saving.
* Nodes can be grouped, where the group can have a name, orientation, and background color. The group can also be a part of another group.
* Highlighting connections when selecting the node. All neighbors and all inbound connections recurse to the root.
* Links are connected to different ports on the node based on the color of the link. Edges with the same color go to the same port.
* Graph may contain cycles, and edges can be bi-directional.

### Widget properties

| Property Type | Name | Type | Description |
| --- | --- | --- | --- |
| Data | Edges | object | Defines edges of graph. |
| Data | Nodes | object | Defines nodes of graph. |
| Events | onSelectionChange | | Allows you to configure one or multiple actions to be executed when the selection is changed. |
| General | Visible | boolean | Controls the visibility of the widget. |
| General | Toolbar | boolean | Hide or show the toolbar, which has zoom and focus options. |
| Style | Background Color | color name or hex | Sets the color of the background |
| Style | Border Color | color name or hex | Sets the color of the border |
| Style | Border width | integer | Sets the width of the border. |
| Style | Border radius | | Rounds the corners of the icon buttons. |
| Style | Box shadow |  | Enables you to cast a drop shadow from the frame of the widget. |
| Style | Layer spacing | integer | Defines the minimal distance between layers (levels of the tree) – from 1 to 500. |
| Style | Node spacing | integer | Defines the minimal distance between nodes - from 1 to 500. |
| Style | Group spacing | integer | Defines the minimal distance between nodes within a group – from 1 to 500. |
| Reference | `nodes` | array | Represents the current nodes in the graph. |
| Reference | `edges` | array | Represents the current edges in the graph. |
| Reference | `isVisible` | boolean | Indicates the visibility state of a widget. |
| Reference | `selectedNodesIds` | array | Represents the currently selected nodes ids. |
| Methods | `setSelectedNodeIds (param: string[]): Promise`​ | | Sets the selected nodes using an array of ids as input param. |

### Wiring Harness

The Wiring Harness widget displays a 2D view of the wiring harness.

<figure markdown="span">
	![The Wiring Harness widget in SPREAD Studio](../src/wiring-harness-widget-on-spread-studio.png)
	<figcaption>The Wiring Harness widget in SPREAD Studio</figcaption>
</figure>

### Widget properties

Missing descriptions.
