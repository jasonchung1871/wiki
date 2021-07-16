You can create fields which will populate based on a calculated value using values from other fields on the form. 

Use the advanced field of the control you wish to populate with a calculated value.

> Try a working example<br>
> [View example](https://chefs.nrs.gov.bc.ca/app/form/submit?f=858a4aba-7e7b-4019-80c1-78a414ee5129)

> Download this example file and [import](Import-Export) it into your design<br>
> [example_calculated_values_schema.json](examples/example_calculated_values_schema.json)

# Data

To designate which data values for a selection should be used for calculated values in other fields, use the `Data` tab.

This is availiable in both basic and advanced controls.

## Select List Example
Drag and drop a `Select List` component into the designer and add some values on the `Data` tab. The label can be what you want the user to see, and the value can be what you would like to be accessible to calculate from in other fields.

![](images/conditional_select_list.png) 

# Calculated Value

## JavaScript
On the field you wish to display the calculated value, navigate to the `Data` tab.

![](images/data_tab.png) 

On the Data tab, scroll down to `Calculated Value` and expand the field. There are some useful help references there.

In the `JavaScript` section enter your calculation for the field you wish to display.

![value = data.myTestRadio * 10;](images/calculated_js.png)

You can use this section to create calculated values of various complexity using JavaScript, referencing one or more existing fields on your form with the `data.*` variable. You can calculate numerical values, build String values, do conditional logic and much more here as required.

If you need to know the field name for a field you wish to base a calculated value on, look at the `API` tab and the `Property Name` box for the name.

![](images/conditional_property_name.png)
