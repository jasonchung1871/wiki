You can show or hide components based on choices a user makes while filling out a form. 

Use the simple settings, or create advanced JavaScript logic.

> Try a working example<br>
> [View example](https://chefs.nrs.gov.bc.ca/app/form/submit?f=9bc36ebf-c6c3-4f5a-9a8d-ea9e8acb0ded)

> Download this example file and [import](Import-Export) it into your design<br>
> [example_conditional_logic_schema.json](examples/example_conditional_logic_schema.json)

# Simple Mode

## Select List
Drag and drop a `Select List` component into the designer and add some values on the `Data` tab. Ensure one has the value "other".

![](images/conditional_select_list.png) 

## Multi-line Text
Drag and drop a `Multi-line Text` component into the designer and go to the `Conditional` tab to select the following options:

![Enter True, the select list, and "other".](images/conditional_multi_line.png) 

## Checkbox
The checkbox component will return `true` or `false` as the value. 

![](images/conditional_checkbox.png)

## Save and view the form
Save and view the form. When you choose "other" from the select list, the "Other" form field will appear.

Conditional logic **does not work** in the form designer view, you must save the form and view it.

# Advanced Mode

## JavaScript
Use JavaScript on the Conditional tab on advanced form components to show or hide elements. This image shows some logic to show or hide a component from choices made in 2 other form fields.

![show = data.checkbox && data.areYouSure == "yes"](images/conditional_js.png)

The "data" variable is the form data object which includes all of the form fields in the design. Access form components by using the Property Name found on each component's API tab.

![](images/conditional_property_name.png)

The checkbox component will return a `true` or `false`. There is no need to compare it to a value.