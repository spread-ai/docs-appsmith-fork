---
Title: Rich Text Editor
Description: Rich Text Editor widget reference
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page provides information on using the Rich Text Editor, which allows you to capture rich text input from users.

## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.

### Data

#### Input Type `string`

Allows you to specify the input type for the **Default Value** property in the widget. You can choose:

Options:

* **Markdown**: This format enables you to use Markdown syntax for styling and formatting the text within the input.
* **HTML**: This format enables you to use HTML markup to structure and style the text within the input.

#### Default Value `string`

Allows you to set the initial text content for the widget.

After selecting an input type as **Markdown** or **HTML**, you can populate the default text section with corresponding content.

```markdown title="Markdown content"
### Markdown

     - Bullet point 1
     - Bullet point 2
     - **Bold text**
     - *Italic text*
```

```html title="HTML content"
<h2>Product Features:</h2>

<ul>
     <li>High-resolution display</li>
     <li>Multiple color options</li>
     <li>Waterproof design</li>
     <li>Advanced security features</li>
</ul>

<p>For more information, please <a href="https://docs.spread.ai">visit our website</a>.</p>
```

### Label

#### Text `string`

Sets the label on the widget.

#### Position `string`

This property allows you to configure the label's placement.

Options:

* **Auto**: Automatically positions the label based on the widget type and layout.
* **Left**: Aligns the label to the left side of the widget.
* **Top**: Positions the label above the widget.

#### Alignment `string`

This property is only available when you select **Left** from the Position property. It allows you to align the text to the left boundary or adjust it closer to the widget using the Right alignment option.

#### Width `number`

This property is only available when you select **Left** from the Position property. It allows you to control the proximity of the text to the widget, determining how close or far it can be positioned.

### Validations

#### Required `boolean`

When enabled, this property makes the Rich Text Editor a mandatory field, When the Rich Text Editor is placed within a Form widget, enabling the **Required** property ensures that the Form's submit button remains disabled until the Rich Text Editor has some value.

### General

#### Tooltip `string`

Enables you to add hints or provide additional information to guide the user regarding the required input.

#### Visible `boolean`

Controls the visibility of the widget. If you turn off this property, the widget would not be visible in View Mode. Additionally, you can use JavaScript by clicking on **JS** next to the **Visible** property to conditionally control the widget's visibility.

For example, if you want to make the widget visible only when the user selects "Yes" from a Select widget, you can use the following JavaScript expression:

```js
{{ '{{Select1.selectedOptionValue === "Yes"}}' }}
```

#### Disabled `boolean`

Prevents users from selecting the widget. Even though the widget remains visible, user input is not permitted. Additionally, you can use JavaScript by clicking on **JS** next to the **Disabled** property to control the widget's disable state conditionally.

For example, if you want to allow only a specific user to fill the input, you can use the following JavaScript expression:

```js
{{ '{{appsmith.user.email=="john@spread.ai"?false:true}}' }}
```

#### Animate Loading `boolean`

Controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property.

#### Hide toolbar `boolean`

Controls the visibility of the toolbar on top of the widget.

#### Height `string`

This property determines how the widget's height adjusts to changes in its content. There are three available options:

* **Fixed**: Maintains a constant height for the widget, allowing you to adjust it by dragging or using the resize handle.
* **Auto Height**: The widget's height adjusts dynamically in response to changes in its content.
* **Auto Height with limits**: Same as **Auto height**, with a configurable option to set the minimum and maximum number of rows the widget can occupy.

### Events

#### onTextChanged

Enables you to specify [supported actions](../../reference/framework/global-functions.md) that would be triggered whenever the user modifies the text input.

## Style properties

Style properties allow you to change the look and feel of the widget.

#### Font color `string`

Represents the text color of the widget, specified as a [CSS color value](https://developer.mozilla.org/en-US/docs/Web/CSS/color). Additionally, the font color can be programmatically modified using JavaScript functions.

#### Font size `string`

Determines the font size of the label. It accepts [CSS font-size](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size) values and can also be programmatically modified using JavaScript functions.

#### Emphasis `string`

Enables you to select a font style for the widget, such as bold or italic. Additionally, the font style can be programmatically modified using JavaScript functions.

#### Border radius `string`

Applies rounded corners to the outer edge of the widget. If JavaScript is enabled, you can specify valid [CSS border-radius](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius) to adjust the radius of the corners.

#### Box Shadow `string`

This property adds a drop shadow effect to the frame of the widget. If JavaScript is enabled, you can specify valid [CSS box-shadow](https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow) values to customize the appearance of the shadow.

## Reference properties

These properties are not available in the property pane, but can be accessed using the dot operator in other widgets or JavaScript functions. For instance, to get the visibility status, you can use `RichTextEditor1.isVisible`.

#### text `string`

The `text` property retrieves the value entered by the user. If no text is entered by the user, the default value would be displayed.

```js
{{ '{{RichTextEditor1.text}}' }}
```

#### isDisabled `boolean`

The `isDisabled` property reflects the state of the widget's Disabled setting. It is represented by a boolean value, where true indicates that the widget is not available, and false indicates that it is enabled for user interaction.

```js
{{ '{{RichTextEditor1.isDisabled}}' }}
```

#### isVisible `boolean`

The `isVisible` property indicates the visibility state of a widget, with true indicating it is visible and false indicating it is hidden.

```js
{{ '{{RichTextEditor1.isVisible}}' }}
```

## Methods

The methods provided by the widget allow users to dynamically update and manipulate its properties, facilitating the creation of dynamic and interactive applications without the need for manual property modifications.

These methods are asynchronous and return a [Promise](../../writing-code-in-studio/using-js-promises.md). You can use the `.then()` block to ensure execution and sequencing of subsequent lines of code in Studio.

#### setVisibility (param: boolean): Promise

Sets the visibility of the widget.

```js
RichTextEditor1.setVisibility(true)
```

#### setDisabled (param: boolean): Promise

Sets the disabled state of the widget.

```js
RichTextEditor1.setDisabled(false)
```

#### setRequired (param: boolean): Promise

Sets whether the widget is required or not.

```js
RichTextEditor1.setRequired(true)
```
