<img class="float-right" src="images/j2c-logo.png" width="200">
# Lab 400 - Add VBCS Web App to call ICS REST API

---

## Introduction

This is the forth of several labs that are part of the **AIC Integration Development** workshop. 

In this lab, you create a VBCS Web Application which calls the REST end-point created in the previous Lab 300.

This is how the VBCS Web Application UI would look like on the completion of this Lab -

  ![](images/vbcs/400/image000_001.png)

Here is a description of what is happening with this web application:

A REST service (post/orders) will be called from a form-based web application. The form will submit an order and has required validations for fields (mandatory/number range/etc.). Also, a custom validation for the entire form before submitting it (using a button) will be built. The order status is returned to the web application.

## Objectives

- Learn how to create a VBCS web application
- Learn how to create form validations, business objects and modify source code
- Learn to change design views and use live mode to create/test data
- Learn how to write custom form validations

## Required Artifacts

- The following lab and an Oracle Integration Cloud account that will be supplied by your instructor
- Completion of the previous *Lab 300*

>***NOTE:*** Use Chrome or IE for the labs preferably, Firefox may cause issues in development

## Build a VBCS web application to call a REST service in ICS

### Login to AIC Integration Home Page

>***NOTE :*** The **User Name** and **Password** values will be given to you by your instructor. See _Lab 100 **1.1.1**: Login to your Oracle Cloud Account_ for more information on how to sign into the AIC Integration home page

------

You will now be presented with the AIC Service Console from which you will be performing the rest of this workshop lab.

### Login to VBCS instance

- Click on the Visual Builder link on the left

  ![](images/vbcs/400/image000.png)

- The Visual Builder console should appear as below

  ![](images/vbcs/400/image001.png)

### Create a VBCS application

- Click **New** to create a new Visual Application

  ![](images/vbcs/400/image002.png)

- Enter `Online Shopping` followed by your initials to uniquely identify the application name. For example - `Online Shopping VL` where `VL` is the suffix and are the first letters of my first and last name. Click **Finish**

  ![](images/vbcs/400/image003.png)
  
- The application dashboard opens and looks like this

  ![](images/vbcs/400/image004.png)

  Check out the various options that can be done using Visual Builder Cloud, viz, **Mobile Apps, Web Apps, Service Connections, etc.**

### Create a Service Connection

- Let us create a service connection (REST) to our service built in Lab 300 as the first step. Click on **Service Connections** and click the **+ Service Connection** button on the left

  ![](images/vbcs/400/image005.png)

- Select **Define by Endpoint** option on the following page

  ![](images/vbcs/400/image006.png)

- Select the **Method** as **POST**, enter the REST endpoint **URL** created in the previous Lab 300 and click **Next**

  ![](images/vbcs/400/image007.png)

- Enter the **Service Name** as `Online Shopping IC` in the **Service** tab

  ![](images/vbcs/400/image008.png)

- Click on the **Authentication Tab**, select **Basic** and enter your ICS **Username** and **Password**

  ![](images/vbcs/400/image009.png)

- On the **Request** tab, select the **Media Type** as **application/json** and enter a sample request payload **Body** -

  ```javascript
    { "OrderId":"1234", "UnitPrice":"10000", "NumberOfItems":"3", "ShippingState":"OH", "Model":"WalkeyTalkey 1.0", "ReturnReason":"Does Not Work" }
  ```

  ![](images/vbcs/400/image010.png)

- Repeat the above step for **Response** tab and enter the following payload under **Body** -
  ```javascript
    {"response":"ORDER_SUCCESSFUL"}
  ```

  ![](images/vbcs/400/image011.png)

- Let us test the service connection and see if the REST service returns a response. On the **Test** tab, click the **Send** button

  ![](images/vbcs/400/image012.png)

- Scroll down and verify that the REST call is successful. A HTTP **200 OK** status is sent back along with a response payload

  ![](images/vbcs/400/image013.png)
  
- Click on **Create** button and the screen should look like this -

  ![](images/vbcs/400/image014.png)

### Create a Web Application

- Back on the **Welcome** page, Click on **Web Apps** and then click on **+ Web Application** on the left

  ![](images/vbcs/400/image015.png)

- Enter the application Id as `ShoppingPortal` followed by your initials to uniquely identify the web application. For example - `ShoppingPortalVL` where `VL` is the suffix and are the first letters of my first and last name

  ![](images/vbcs/400/image016.png)

- The screen should look like this -

  ![](images/vbcs/400/image017.png)

  This is a right time to check out the various designs views, tools, components, etc. available in the application console

- You can swtich between design views as shown below. Choose the right view that fits your style of coding/design

  ![](images/vbcs/400/image017_001.png)

- Let us create a web form now to hold the fields required to create/process an order by dragging and dropping components from the component palette on the left

- Drag and drop a **Heading** component which is the first of the components under **Common** elements. You can also filter components to find a component quickly

  ![](images/vbcs/400/image018.png)

- Click on the property tab, you will find this towards the upper right of the screen -

  ![](images/vbcs/400/image019.png)

- Name the **Text** property as `Manage Orders` and make the heading **Level** as **H2**

  ![](images/vbcs/400/image020.png)

- Drag and drop a **Horizontal Rule** under the heading

  ![](images/vbcs/400/image021.png)

- Repeat the step above for adding a **Panel** on to the page

  ![](images/vbcs/400/image022.png)

- Again, drag and drop a **From Layout** inside the **Panel** to create our form components

  ![](images/vbcs/400/image023.png)

- Edit the form properties and set **Max Columns** to **1** and **Label Edge** to **Start**

  ![](images/vbcs/400/image024.png)

- Drag and drop an **Input Text** component inside the **Form Layout**

  ![](images/vbcs/400/image025.png)

- Set the properties of the **Input Text** by naming **Label Hint** as `Order ID` and checking the **Required** checkbox. Selecting **Required** will make the form field mandatory marked by an asterix (**_*_**)

  ![](images/vbcs/400/image026.png)

- Drag and drop a **Number** component below Order ID. Note the drop position, which is below the **Input Text** and inside the **Form Layout**. The editor highlights the drop position in blue

  ![](images/vbcs/400/image027.png)

- Edit the properties as below -
  
  **Label Hint** - `Quantity (1 - 10)`
  
  **Min** - `1`
  
  **Max** - `10`

  **Required** - `Checked`

  ![](images/vbcs/400/image028.png)

  Note here that we have set the **Min** and **Max** properties, and this will be validated at runtime

- Drag and drop a **Currency** component below Quantity (1-10)

  ![](images/vbcs/400/image029.png)

- Set the properties as below - 

  **Label Hint** - `Price`

  **Min** - `0`

  **Max** - `1000`

  **Step** - `100`

  **Required** - `Checked`

  ![](images/vbcs/400/image030.png)

  ***Scroll down here***

  **Converter** - `$`

  **Currency Code** - `USD`

  **Currecy Display** - `Symbol`

  **Currency Format** - `Standard`

  **Minimum Integer Digits** - `1`

  **Minimum Fraction Digits** - `0`

  **Maximum Fraction Digits** - `2`

  **Thousands Separator** - `Checked`

  ![](images/vbcs/400/image031.png)

- Drag and drop a **Select One** below price, set **Label Hint** to `Ship To` and check the **Required** checkbox

  ![](images/vbcs/400/image032.png)
 
- Now let us drag and drop another **Input Text** in between Order ID and Quantity

  ![](images/vbcs/400/image033.png)

- Set the **Label Hint** to `Model` and **Placeholder** to `Ex: walkie Talkie 1.0`

  ![](images/vbcs/400/image034.png)

- Drag and drop a **Text Area** below Ship To

  ![](images/vbcs/400/image035.png)

- Set the **Label Hint** to `Return Reason`, **Placeholder** as `Reason if this order is a return.` and set **Rows** to `3`

  ![](images/vbcs/400/image036.png)

- Now is a good time to see how our form looks in real-time. Click on **Run** icon on the top right corner

  ![](images/vbcs/400/image037.png)

- The UI form should look similar to this - 

  ![](images/vbcs/400/image038.png)

### Create a business object

Let us now create a business object to hold the Ship To locations and later on bind it to the **Select One** component created in the previous section

- Click on the business objects icon on the left-most icon pane and click **+ Business Object**

  ![](images/vbcs/400/image039.png)

- Enter the **Label** as `ShipToLocationLOV` and click the tick-mark to create a business object

  ![](images/vbcs/400/image040.png)

- Check the various tabs available in the created business object

  ![](images/vbcs/400/image041.png)

- On the **Fields** tab, see that a few default fields have already been created along with the business object. Let us add a new field to hold the states for Ship To location, click on **+ New Field**. Set the **Label** as `State` and type as **String** with the **`A`** icon. Click the tick-mark to create a new field

  ![](images/vbcs/400/image042.png)

- Let us add a few rows to the business object inside the **Data** tab. Click on **+ Add Row**

  ![](images/vbcs/400/image043.png)

- Enter the **State** as `AK` and click the tick-mark

  ![](images/vbcs/400/image044.png)

- See that the row is created and the ID is auto-populated

  ![](images/vbcs/400/image045.png)

- Let us explore another method to upload data through a CSV file. Create a `states.csv` file (if you have not received the same from your instructor). The contents should be as below -

  ```javascript
    State
    CO
    DE
    FL
    GA
    HI
    IL
    KS
    LA
    MO
  ```

- Click on the import icon ![](images/vbcs/400/image045_001.png), upload the `states.csv` file just created, select the **Append** option and click on **Import**.

  ![](images/vbcs/400/image046.png)

- Check the status and make sure the status shows green ticks. Click **OK**

  ![](images/vbcs/400/image047.png)

- Verify that all the rows from the csv are updated and the existing row created (with ID 1) is not overwritten

  ![](images/vbcs/400/image048.png)

### Bind data-bound components to Business Objects and create variables to hold form fields

- Back in our UI design view, select the Ship To **Single Select**. Open the properties and click on the human icon towards the right corner

  ![](images/vbcs/400/image049.png)

- Click on **Add Options**. Expand and select the **GET** endpoint of the **Business Object** (ShipToLocationLOV) just created. Click **Next**

  ![](images/vbcs/400/image050.png)

- Check **state** on the left hand side under `response/items/item[i]` and select **state** for both **Value** and **Label** on the right hand side. Click **Next**

  ![](images/vbcs/400/image051.png)

- Leave defaults since there are no query parameters for this object and click **Finish**

  ![](images/vbcs/400/image052.png)

- Check that the **Options** property under **Data** tab in the properties of the **Single Select** is updated as `[[$page.variables.shipToLocationLOVListServiceDataProvider]]` to point to ShipToLocationLOV

  ![](images/vbcs/400/image053.png)

- Let us now use a new feature called the **Live** mode and test if the data is really being populated from ShipToLocationLOV. Click on **Live** and see that the Ship To shows the options from the business object ShipToLocationLOV

  ![](images/vbcs/400/image054.png)

- It is good time to experiment with the source code now. Click on **Live** again to exit the **Live** mode. Click on **Code** to see the source that is being generated while we are designing the UI using a visual drag and drop approach

  ![](images/vbcs/400/image055.png)

- Drag and drop a **Horizontal Rule** after the **Form Layout** under the **Panel**

  ![](images/vbcs/400/image056.png)

- Drag and drop a **Button** after the **Horizontal Rule** under the **Panel**. The area where the **Button** would be placed would be highlighted in a darker shade of blue. See the screenshot below -

  ![](images/vbcs/400/image057.png)

- Change the **Text** property of the button to `Submit Order`

  ![](images/vbcs/400/image058.png)

- Let us create the required data types and variables to hold and submit data now. Click on variables icon on the left and click the **Types** tab. Click **+ Type** and select **From Endpoint**

  ![](images/vbcs/400/image059.png)

- Expand **Service Connections** and select the **POST** service from **OnlineShoppingICS**. Click **Next**

  ![](images/vbcs/400/image060.png)

- Name the type as `postOrders`, select **Request** under **Endpoint Structure** and click **Finish**

  ![](images/vbcs/400/image061.png)

- Click **+ Type** and select **From Endpoint** again to create another variable of response type

  ![](images/vbcs/400/image062.png)

- Name it `postOrdersResponse`, select **Response** under **Endpoint Structure** and click **Finish**

  ![](images/vbcs/400/image063.png)

- Verify that the two variables are created

  ![](images/vbcs/400/image064.png)

- Click **Variables** tab. Let us add variables to hold the data for all the form fields. Click **+ Variable**

  ![](images/vbcs/400/image065.png)

- Name the variable `orderInfo` and select the type as **postOrders**. Click **Create**

  ![](images/vbcs/400/image066.png)

- Verify that the variable is created and click **+ Variable** to create another variable

  ![](images/vbcs/400/image067.png)

- Name the variable `reponseCode` and select the type to be of **postOrdersResponse**. Click **Create**

  ![](images/vbcs/400/image068.png)

- Click **+ Variable** to create another variable. Name the variable `orderID` and select the type to be of **String**. Check **Create Another** checkbox and click **Create**

  ![](images/vbcs/400/image068.png)

- Repeat the previous step to create the following variables -

  `model`, `returnReason`, `shipTo` of type **String**

  `price`, `quantity` of type **Number**

  The screen should look like this after all the variables are created -

  ![](images/vbcs/400/image069.png)
  
- Back in the design view, select **Order ID**, click **Data** tab under the property window

  ![](images/vbcs/400/image070.png)

- Open expression builder icon and select **orderID** as the **Value** for the **Input Text**. Note that you may need to click the reload icon if the variables created fail to appear under the expression builder

  ![](images/vbcs/400/image071.png)

- Verify that the **Value** is updated to `{{ $page.variables.orderID }}`

  ![](images/vbcs/400/image071.png)

- Repeat the above step for all the form fields and verify the **Value** is as follows -

  **Model** - `{{ $page.variables.model }}`

  **Quantity** - `{{ $page.variables.quantity }}`

  **Price** - `{{ $page.variables.price }}`
  
  **Ship To** - `{{ $page.variables.shipTo }}`
  
  **Return Reason** - `{{ $page.variables.returnReason }}`

### Map fields and variables to call the REST endpoint

- Click on the **Button** and open the property inspector. Click **+ New Event** and select **Quick Start: 'click'**. This means that an **Action Chain** will be triggered when the button is clicked

  ![](images/vbcs/400/image073.png)

- Let us design the **Action Chain** to submit the form on button click. Drag and drop an **Assign Variables** action onto the flow below **Start** onto the **`+`** icon

  ![](images/vbcs/400/image074.png)

- In the property inspector, click on the **Assign** link to assign and map variables

  ![](images/vbcs/400/image075.png)

- Click on `model` under **Page** variables on the left-hand side and drag and drop it to `Model` under `orderInfo`

  ![](images/vbcs/400/image076.png)

- Map the following fields similar to the above step -

  `orderID` -> `orderInfo/OrderId`

  `quantity` -> `orderInfo/NumberOfItems`

  `price` -> `orderInfo/UnitPrice`

  `shipTo` -> `orderInfo/ShippingState`

  `returnReason` -> `orderInfo/ReturnReason`

  The sreen will look like this after the mappings -

  ![](images/vbcs/400/image077.png)

- Check that the `orderInfo` variable is mapped under **Variables**. Drag and drop a **Call Rest Endpoint** unto the **`+`** icon under the assign

  ![](images/vbcs/400/image078.png)

- Click on **Select Endpoint**

  ![](images/vbcs/400/image079.png)

- Expand **Service Connections** and select the **POST** service from **OnlineShoppingICS**. Click **Select**

  ![](images/vbcs/400/image080.png)

- See that the parameters are in the **NOT MAPPED** status. Click on the **Assign** link to assign the parameters

  ![](images/vbcs/400/image081.png)

- Map the `orderInfo`on the left-hand side under **Page** variables to `body` on the right-hand side under **Parameters**

  ![](images/vbcs/400/image082.png)

- Add another **Assign** to assign the return value from the REST service call. This time drop it on the **`+`** icon next to the **Call Rest Endpoint** and not below it

  ![](images/vbcs/400/image083.png)

- Drag another **Assign** on the left side **`+`** icon below **Call Rest Endpoint**

  ![](images/vbcs/400/image084.png)

- Now let us assign the return values from the REST call. Click on the **Assign** under `success`, and click the **Assign** link beside **Variables**

  ![](images/vbcs/400/image085.png)

- Drag and drop the `response` element under **Results** on the left to `responseCode/response` on the right under **Page** variables

  ![](images/vbcs/400/image086.png)

- Repeat the two steps above for the **Assign** under `failure`. This time, instead of dragging and dropping an element, paste the following snippet for the **Page** variable `responseCode` on the right -
  
  ```javascript
    {
    "response": "Failure"
    }
  ```

  ![](images/vbcs/400/image087.png)

- The final **Action Chain** would look similar to this -

  ![](images/vbcs/400/image088.png)

### Test the entire Web Application

We can test the application in **Live** mode or by clicking the **Run** icon on the top right corner which opens the form in a new browser window. To test the application, we need to capture the response and display it somewhere so that we know what is happening behind the scenes, whether the REST endpoint was called, whether the call was successful or the call failed. We can achieve this simply by using a **Text** component and setting the value of the component to the reponse payload from the web-service call.

- Drag and drop a **Text** component. You can use the **Filter** option to find it quickly

  ![](images/vbcs/400/image089.png)

- Open up the expression builder and set the **Value** property of the **Text** component to `responseCode/response`

  ![](images/vbcs/400/image090.png)

- Verify that the value is updated to `{{ $page.variables.responseCode.response }}`

  ![](images/vbcs/400/image090_001.png)

- Either select the **Live** mode by clicking ![](images/vbcs/400/image091_001.png) or click the **Run** ![](images/vbcs/400/image091_002.png) icon to open the form in a new browser tab

- Play around the form and try entering various values, wrong values, empty values and for the various form fields. You can see that the validations we created on the form fields are at play after tabbing out or after the form field loses focus. Click on the **Submit Order** with the following input -

  ```javascript
    Order ID      : 1
    Model         : Test
    Quantity      : 1
    Price         : 1000
    Ship To       : CO
    Return Reason : (Optional - any random text)
  ```

  You can see the web-service (REST) call goes through and a status is returned such as`ORDER_SUSPENDED` or `ORDER_PROCESSED`

  ![](images/vbcs/400/image092_002.png)

- Enter wrong values and see that the validation happens. For example -

  ```javascript
    Order ID      : (blank)
    Model         : (blank)
    Quantity      : -100
    Price         : 100000
    Ship To       : (not selected/blank)
    Return Reason : (Optional - any random text)
  ```
  You can see the web-service (REST) call goes through but no status is returned; the form validation is at play and the status of `Failure` that we set in the **Action Chain** is used and printed on the UI this time

  ![](images/vbcs/400/image092_001.png)

  ***NOTE :*** Enter a different **Order ID** every time you click on the **Submit Order** button so that the REST endpoint returns a valid value.

Let us alter the flow in the next section so that the form is submitted only when all the form fields are validated.

### Add Client-Side Validation to the form

First we have to set up our form to check the validity of its contents before submitting. We do this by surrounding the form with an `<oj-validation-group>` element, adding a custom isFormValid Javascript function that returns a boolean, and then calling that function before submitting the form.

Now it is time to experiment directly on the source and add some code!

- Click on the **Code** button and view the source code that has been generated till now

  ![](images/vbcs/400/image093.png)

- Surround the form **div** with `<oj-validation-group id="orderForm">`. Don't forget the closing tag

  ![](images/vbcs/400/image094.png)

- Now the page won't load because we haven't imported the `oj-validation-group` component. Switch to the **Code** view -

  ![](images/vbcs/400/image095.png)

- Add the following section in bold to the bottom of the imports section:

  ![](images/vbcs/400/image096.png)
  
  ```javascript
    "oj-validation-group": {
        "path": "ojs/ojvalidationgroup"
      }
  ```

  Note the **`,`** (comma) before adding the value above

- Click on the `shoppingportal` application on the left and switch to the **JS** view to add Javascript. Add the following function -

  ```javascript
      AppModule.prototype.isFormValid = function(form) {
      var tracker = document.getElementById(form); 
      if (tracker.valid === "valid") {
        return true;
      } else {
        tracker.showMessages();
        tracker.focusOn("@firstInvalidShown");
        return false;
        }
      };
  ```

  ![](images/vbcs/400/image097_001.png)

- Let us change the **Action Chain** on button click to call this form validation function. Click on **Actions** and click on **ButtonClickAction**

  ![](images/vbcs/400/image098.png)

- Drag and drop an **If** under **Logic** to the line below **Start**

  ![](images/vbcs/400/image099.png)

- Now, move the **Assign Variables orderInfo** onto the **`+`** icon under the **true** branch of the **If** as shown below -

  ![](images/vbcs/400/image100.png)

- Click on the **If** and set the **Condition** property to `{{ $application.functions.isFormValid("orderForm") }}`. This will call the form validation Javascript function that we previously wrote

  ![](images/vbcs/400/image101.png)

- The final **Action Chain** looks as below -

  ![](images/vbcs/400/image102.png)

- Now run the form again by clicking the **Run** ![](images/vbcs/400/image091_002.png) icon. Click the **Submit Order** button without filling any of the form fields and see that the form does not get submitted this time and the REST endpoint is not called but the entire form is validated

  ![](images/vbcs/400/image103.png)

- Fill in the form fields and click **Submit Order** and verify that the REST endpoint is called successfully and a valid status is returned

  ![](images/vbcs/400/image104.png)
---

You have now completed the first VBCS Lab (400) from the AIC Developer Workshop.

Congratulations! You should now have a much better understanding of how to work with VBCS to create web applications.
