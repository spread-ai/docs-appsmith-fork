---
title: How to work with data in the UI
description: How to work with data when creating Studio applications
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

## Synopsis

This tutorial takes you through the process of viewing and editing individual records via forms when creating applications in SPREAD Studio.

## Prerequisite knowledge

- [x] An understanding of how to [create Studio applications](../creating-studio-applications.md).
- [x] Access to a SPREAD Studio environment.

## Instructions

### Create the form

#### 1. Create the form

On the **UI** tab inside the Studio workspace, select **+ New UI element** and drop a **Form** widget and a **Table** widget on the canvas.

#### 2. Add widgets to view details

Now add widgets on the form to view user details:
    * For the user's name, drop an **Input** widget inside the Form. 
    * On the property pane to the right, select on the default name **Input1** and rename it to `nameInput`. 
    * In the **Text** property box, enter `Name`. 
    * In the **Default Value** property box, type `{{ '{{usersTable.selectedRow.name}}' }}`. This displays the user's name of the selected row on the **usersTable** Table widget.

You also need to view the user's date of birth: 
    * Drop a **Datepicker** widget inside the Form. 
    * Rename the widget to `dobInput`.
    * In the **Text** property box, enter `DOB`.
    * select the **JS** button next to the **Default Date** property to connect the Datepicker widget to the user's date of birth on the Table. 
    * Type `{{ '{{usersTable.selectedRow.dob}}' }}` in the **Default Date** property box.
    * In the **Date format** property, select the **LL** date format.

And finally to view the user's photo, drop an **Image** widget inside the Form. In the **Image** property box, type `{{ '{{usersTable.selectedRow.image}}' }}`.

You've completed binding the data to the widgets on the Form. Select the rows on the Table to view the corresponding user details on the Form.

### Update records

#### 3. Select the Queries tab

Select the **Queries** tab on the **Entity Explorer** to the screen's left. 

#### 4. Create a new query

Select the **+ New Query / API** button.

#### 5. Select the tutorial query
 
Select **usersTutorialDB query** from the list of options. Rename the query to `updateUsers`. Delete the default fetch query template.

!!! warning "Test database"
  The databases used in tutorials are public and shared by all Appsmith users, so ensure that you don't input confidential information during testing. The databases are automatically reset every day, so any updates made to these databases are temporary.

#### 6. Update users

Paste the  SQL update command into the query editor to update the `users` table in the database with the details modified in the Form.

  ```sql
  UPDATE users 
  SET name = {{ '{{nameInput.text}}' }},
  dob = {{ '{{dobInput.selectedDate}}' }}
  WHERE id = {{ '{{usersTable.selectedRow.id}}' }} 
  ```

### Trigger update on button click

#### 7. Go back to the canvas

 Go back to the canvas by clicking on the **UI** tab on the **Entity Explorer**.

#### 8. Connect query to button

To connect the **updateUsers** query to a button, select the default **Submit** button on the Form:
    * On the property pane to the right of the screen, in the **Label** property box, change the label to `Update`.
    * Select the **+** icon next to the **onClick** event. 
    * In the **Action** list, select **Execute a query > updateUsers** to run the query on button click.
    * Select the **+** icon next to the **onSuccess** callback. 
    * Select **Execute a query > getUsers**. 

The button is now configured to execute the **updateUsers** query to save any modified user details on the Form and to refresh the Table widget with the updated information. 

#### 9. Test the update button

Select the first row on the Table. Go ahead and modify the user's name on the Form and test the **Update** button to see if the update worked.
