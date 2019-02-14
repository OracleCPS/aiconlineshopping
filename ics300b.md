<img class="float-right" src="images/j2c-logo.png">

# **Lab 300 - Part B: Oracle Integration Cloud (OIC) Development Workshop**

## **Introduction**

In this Lab, we will be using Oracle Integration Cloud (OIC) to add additional components to finish the flow of a sample integration.

The integration flow that we will be working to build is depicted below:

![](images/300b/onlineshoppingimage.png)

## **Objectives**
- Complete the sample integration by adding two conditional branches to the flow

### **Pre-Requisites**
- **REQUIRED:** 
    - This lab assumes that you have already completed [Lab300A](/ics300a.md)

## **Required Artifacts**

- The following lab 
- An Oracle Cloud account (supplied by your instructor)

# **Online Shopping Integration Development**

## **300b.1: Login to your Oracle Cloud account**

**300b.1.1**: Navigate to the Home Page by using the OIC URL provided to you by your instructor. The URL should have the following pattern: 
https://{**InstanceName**}-{**CloudAccountName**}.integration.ocp.oraclecloud.com/ic/home/

**300b.1.2**: Log in using the IDCS re-route page

![](images/300b/image002.png)  

**300b.1.3**: From the home page, select *`Integrations`* and you should be auto redirected to the Integration Designer Page where you will see a list of the all the integrations available on the environment

![](images/oic-1.png)

## **300b.2: Clone and Develop your Integration**

**300b.2.1:** Using the existing integration named **Online Shopping App Sample**, create a clone integration 
> Search with above integration name as shown below 

![](images/300b/img102.PNG)

**300b.2.2:** Select the hamburger icon <img src="images/menu.svg"> on the right and click **`Clone`** as shown below 

![](images/300b/img103.png)

**300b.2.3:** A window will open where you will provide the integration name as instructed by your proctor and a description if you wish then, click the **`Clone`** button as shown in the below diagram

![](images/300b/img104.png)

> A new integration is created and it will have a mini banner with the word **_NEW_** next to it

![](images/300b/img105.png)

**300b.2.4:** _Now, we will add two conditional branches in the same flow and test it out_
- Click on the integration name to reveal an existing workflow.

![](images/300b/img106.png)

**300b.2.5:** Select the **`Switch` icon** on left and click **`+`** sign that appears 

![](images/300b/img107.png)

**300b.2.6:** A new branch will be created and the numbered paths will be renumbered

![](images/300b/img108.png)

**300b.2.7** Click on the `pencil icon` to edit this condition

![](images/300b/img109_1.png)

**300b.2.8a:** You will be redirected to provide the expression. Give the **Expression Name** 
> **CreditCheckSuspended**

![](images/300b/img110.png)

**300b.2.8b:** Next, we need to select the input paramater
- Drill down in the Source under ***$CheckCredit*** and select **<> \*response** to drag and drop on the empty box above on the left

![](images/300b/img111.png)

**300b.2.8c** Provide the expression parameter
> **"CREDIT_CHECK_SUSPENDED"** 
- Click on **`Validate`** and wait for the success message before closing

![](images/300b/img112.png)

**300b.2.9:** Next, we need to map the output parameters
- Click on the `flag icon` to reveal a list of actions

![](images/300b/img113.png)

- Select and drag **`Map`** from the list of Data actions to the line immediately following the second path

![](images/300b/img114.png)

**300b.2.10:** Select the `map icon` and click the `pencil` to open the mapping configuration page 

![](images/300b/img115.png)

**300b.2.11a:** Expand the Target side of the window until ***<> \*response*** is revealed then click on the field

![](images/300b/img116_1.png)

**300b.2.11b:** Click on the field below the element in the mapping statement to enter the following: 

> **ORDER_SUSPENDED** 

- Click `Save` at the top followed by `Close` at the bottom to be returned to the configuration page

![](images/300b/img117.png)

- Click `Validate` and when prompted with a success message, click `Close`

![](images/300b/img117_1.png)

**300b.2.12:** 
- Click on the **`flag icon`** to reveal a list of actions
- Select and drag **`Return`** from the list of End actions to the line immediately following the second path

![](images/300b/img118.PNG)

- Since we previously set up the mapping, delete the repeated one
    - Click on the icon
    - Select the hamburger icon
    - Click on delete
    - Confirm delete in the modal

![](images/300b/img119_1.PNG)

> Your overall setup should look like this which completes our first - **if/else** logic

![](images/300b/img119.PNG)

**300b.2.13:** Next, click on the `bullseye icon` <img src="images/bullseye-invoke.png" width="25px"> to reveal a list of invoke connections configured
- Select and drage **REST** connector: `OnlineShoppingPaymentInvoke` to the third (3) conditional labeled ***Otherwise***

<img src="images/300b/img120.png" width="350px">

<img src="images/300b/img121.png" width="400px">

**300b.2.14:** A wizard will open where you will provide the details as marked in red. Once completed, click **`Next`** to continue to the *Request Parameters* tab

![](images/300b/img122.png)

**300b.2.15:** On the *Request Parameters* tab, add two input fields for the request mapping
- Click on **`+`** icon to add each parameter as shown below (OrderId and PaymentAction) with both set to data type string
- Then, click **`Next`** to continue to the _Response_ tab

![](images/300b/img123.png)

**300b.2.16:** On the *Response* tab:
- Select **`JSON Sample`** for the format 
- Click **`<<< inline >>>`** (marked in red below)

![](images/300b/img124.png)

- On the *Enter a Sample JSON* window, enter the following:

`````json
{
    "response": "PAYMENT_FAILED"
}
`````

- Then click **`Ok`** to return the previous window where you will click **`Next`** to continue to the _Summary_ tab

![](images/300b/img125.png)


**300b.2.17:** On the *Summary* page, check all the configurations we've completed and click **Done** to exit from here and return to the integration flow

![](images/300b/img127.png)

**300b.2.18:** Along with the node we configured, a mapping capability is automatically generated
- Click on the `pencil` icon to **edit** the mapping

![](images/300b/img128.png)

![](images/300b/img129.png)

**300b.2.19a:** You will be redirected to a configuration window where you will: 
- Drill down into the Target ***<> \*execute*** to reveal the **Query Parameters**
- Click on `PaymentAction` to be redirected to an expression builder
- Update the PaymentAction mapping statement with the value as shown below
- Then select `Save` at the top and `Close` at the bottom to return to configuration

![](images/300b/img130.png)

**300b.2.19b:** Map **OrderId** from the ***Source*** under request-wrapper to **OrderId** in the ***Target*** under *Query Parameters* 
- Once done, click **`Validate`** to verify all the mappings

AND
- Select **`Close`** to exit from this page and return to the integration flow

![](images/300b/img130_1.png)

**300b.2.20:** To complete this path, add an *end* action

- Click on the `flag icon` to reveal a list of actions 

![](images/300b/img131.png)

- Select and drag **`Return`** from the list of _End_ actions to the line immediately following the _DeclinePayment_ REST connection

![](images/300b/img132.png)

**300b.2.21:** Select the `map icon` and click on the `pencil icon` to open the mapping configuration page

![](images/300b/img133.png)

**300b.2.22:**  On the configuration page:

- Drill down into the Target fields until ***<> \*response*** is revealed then click on that field which will redirect you to an expression builder
- Click on the field below the element in the mapping statement and enter the following string:

    > **ORDER_SUSPENDED** 

- Click `Save` at the top followed by `Close` at the bottom to be returned to the configuration page
- Click `Validate` and when prompted with a success message, click `Close`

![](images/300b/img134.png)

![](images/300b/img134_1.png)

**300b.2.23:** Click on **`Save`** and then **`Close`** to exit the integration design canvas

![](images/200/image045.png)

**300b.2.24:** Find your integration in the list and click on the `slider` <img src="images/200/image047.png" width="30px"> next to your integration to activate

![](images/300b/img143.png)


**300b.2.25:** On the **Activate Integration** confirmation window:
- Select **Enable Tracing** then **Include payload**
- Click **`Activate`**

![](images/300b/img144.png)

- The slider should turn green once active

![](images/300b/img145.png)

**300b.2.26:** Once your integration is activated, select Cogwheel <img src="images/gear.png" width="20px"> button and click on the given Endpoint URL

![](images/300b/img145_1.png)

**300b.2.27:** You will be redirected to a new page _ENDPOINT DESCRIPTION_. 
- Copy the `Endpoint URL` and save it for later. We suggest pasting it in a text editor or note taking app. It will be used in the next section in Postman for testing your integration.
- Make a note of the METHOD
- Copy the Request Sample
![](images/300b/img145_2.png)
![](images/300b/img145_3.png)

## **300b.3: Testing your Integrations**

**300b.3.1a:** Click on the `Collection` tab as shown below and provide a name for your collection as shown below  
![](images/300b/img146.png)

![](images/300b/img146_1.png)

**300b.3.1b:** Click on the `AddRequest` menu item as shown below

![](images/300b/img146_2.png)

**300b.3.2:** On the window that opens, provide the name of the Integration and optionally, a description then, click **`Save`**

![](images/300b/img147.png)

**300b.3.3:** In the builder window, click on the **`Authorization` Tab**
- For Authorization type, select Basic Auth
- Provide the credentials given to you by your instructor

![](images/300b/img148.png)

**300b.3.5:** Next, we need to set the request.
- Select `POST` for the HTTP Verb 
- Copy and paste the Endpoint URL that you previously saved (step 300b.2.39)
- Click on the **`Body`** section 
    - select the **`raw`** radio button
    - choose ***`JSON (application/json)`*** from the dropdown

```json
{"OrderId": "1235", "UnitPrice": "10000", "NumberOfItems": "3", "ShippingState": "OH", "Model": "WalkeyTalkey 1.0", "ReturnReason": "Does Not Work"}
```

![](images/300b/img148_1.png)

**300b.3.6:** Click on the `Send` Button and check the response in the pane below

![](images/300b/img150.png)

![](images/300b/img137.png)

**300b.3.7:** Navigate back to the Integration Page and go to the **Tracking** field as shown below 

![](images/300b/img152.png)

![](images/300b/img152_1.png)

![](images/300b/img152_2.png)

**300b.3.8:** Click on the order instances as shown

![](images/300b/img153_1.png)

**300b.3.9:** You will see the overall flow of the integration as shown 

![](images/300b/img154_1.png)

--- 

# **THIS LAB IS NOW COMPLETED**
> In the next lab, we are going to create a User Interface using Visual Builder Cloud Service (VBCS), then call the REST API with online shopping request.