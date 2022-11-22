Navigation ability can be added to your forms using the ‘Tabs’ component and programming ‘Button’ components to switch those tabs.

![nav1](https://user-images.githubusercontent.com/91633223/203415099-cc0d93df-4a37-4261-90e8-4b6b25d2626e.png)

![nav2](https://user-images.githubusercontent.com/91633223/203415103-e29d6ae4-f009-4936-bbb5-d5def4f9c4cd.png)

**Step 1**: Add a ‘Tabs’ component to the form and customize the tabs based on your requirements. 

![nav3](https://user-images.githubusercontent.com/91633223/203415241-980110ae-4be5-4e5d-946a-93e15d1e84d5.png)

**Step 2**: Add two ‘Button’ components that will switch the tabs back and forth. In this case, they are named ‘Previous’ and ‘Next’

**Step 3**: Click on the Settings (gear) icon for each button, and select the ‘Custom’ option from the ‘Action’ dropdown in the ‘Display' tab.

![nav4](https://user-images.githubusercontent.com/91633223/203415419-572e347d-10c4-4512-bdaa-6e3a1d442092.png)

**Step 4**: Add the following code in the ‘Button Custom Logic’ field

```
const tab = form.getComponent('tabs');
const index = tab.currentTab;
tab.setTab((index-1));
window.scrollTo(0,0);
```

![nav5](https://user-images.githubusercontent.com/91633223/203415546-b9e5223f-7c3e-44ef-a857-19fffc4baef0.png)

**Step 5**: Similarly, add the following code to the ‘Button Custom Logic’ section for the ‘Next’ button

```
const tab = form.getComponent('tabs');
const index = tab.currentTab;
tab.setTab((index+1));
window.scrollTo(0,0);
```

Save your changes and the buttons are now programmed to switch the tabs within the form. 
