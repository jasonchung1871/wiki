A custom progress bar can be added to the form to enhance the user experience and indicate the remaining steps within the form. More features have been added to advance the functionalities of the progress bar.

**Features added**

- ability to perform validity checks on all the components ( e.g. input component) in each tab component
- ability to indicate error colour in case the validity checks fail
- each progress bar step has a title that corresponds with the title of each tab of the tab component

---

### Type A: Progress Bar with Tab Component

This Progress Bar is designed to work with Tab Component, and with the Next and Previous Buttons

![ap1](https://user-images.githubusercontent.com/91633223/204036758-601b0034-ea20-439f-972d-b86285fa895a.png)

---

### Type B: Progress Bar with any Layout Component

This Progress Bar is designed to work with any layout component and with the Next and Previous Buttons. Its functionality has been developed almost similarly to Formio Wizard.  You switch between each layout using the Previous and Next buttons. It uses the `hide` attribute of each layout by setting it to true or false and using the triggerRedraw function to redraw the component to the screen.

![ap2](https://user-images.githubusercontent.com/91633223/204036962-61c5845e-366f-4caf-8a6b-99b8e9f12196.png)


