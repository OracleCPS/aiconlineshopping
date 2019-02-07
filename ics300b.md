<img class="float-right" src="images/j2c-logo.png">

# **Lab 300 - Part B: Online Shopping Integration Development**

## **Introduction**

In this Lab we are going to take a sample integration flow and add additional components to finish the flow.

The AIC integration flow that we'll be building is shown in the following picture:

![](images/300b/onlineshoppingimage.png)
---
## **Objectives**
Take sample integration flow and add 2 conditional branches and test.

## **Required Artifacts**

- The following lab and an Oracle Public Cloud account that will be supplied by your instructor.

## Login to your Oracle Cloud account

### Login to OIC Integration Home Page

>***NOTE:*** the **User Name** and **Password** values will be given to you by your instructor. See _Lab 100 **1.1.1**: Login to your Oracle Cloud Account_ for more information on how to sign into the OIC home page

![](images/200/image086.png)

### REST Connection

In this first part of the lab, we will reuse an existing connection :

Let’s start by logging into the Oracle Cloud account using your allocated user   

**2.1** Click on **Itegrations** tab followed by  the **Connection** section from designer page as shown below 

![](images/200/img112.png)

![](images/200/img113.png) 

**2.2** We are already having a connection named "OnlineShoppingPaymentInvoke".Will use the same  during our developement.

![](images/300b/image101.png)

**2.3** Click on the **Integrations** link in the upper left to get back to the Integration page

![](images/200/img088.PNG) 

### Clone and Develop your Integration

**1.1** You are already having an existing integration named **Online shopping Sample**.We will create a clone of the same one.

**1.2** Search with above integration name as shown below 

![](images/300b/img102.PNG)

**1.3** Select the hamburger icon the right and Click **Clone** as shown below 

![](images/300b/img103.png)

**1.4** A new page comes up.Provide the integration name as per your choice ,description if you wish to and Click **Clone** button as shown in the below diagram

![](images/300b/img104.png)

**1.5** A new integration is created as shown below 

![](images/300b/img105.png)

_Now we will add two conditional branches in the same flow and test it out_

**1.6** Click on the newly selected integration and you will see already an exsting workflow.Here we will add two conditional branches and test it out.

![](images/300b/img106.png)

**1.7** Select **switch button** on left and click **+** as shown below 

![](images/300b/img107.png)


**1.8** A new branch will be created as shown below in below diagram 

![](images/300b/img108.png)


**1.9** Click on the edit button as shown below

![](images/300b/img109_1.png)

**1.10** A new page comes up,provide **Expression Name**  as shown below 

![](images/300b/img110.png)

**1.11** Next we need to select the input paramater.Drill down and select **response** field and drop on empty box as shown below

![](images/300b/img111.png)

**1.12** Finally provide the expression parameter as shown below and click on **Validate** button.Your overall page should look like this 

![](images/300b/img112.png)

**1.13** Click **Close** button to come out of this wizard. Next we need to map the output parameters. Select **Map ** Data from Actions tab as shown 

![](images/300b/img113.png)

**1.14** Drag **Map Data** and place in swimlane as shown below

![](images/300b/img114.png)

**1.15** Select Map data and click on 'Edit' button as shown below

![](images/300b/img115.png)

**1.16** Mapper page will appear. Exapand the response mapper as shown below.

![](images/300b/img116_1.png)

**1.17** Update the response mapper with below mentioned field. Click on validate to finish the setup.

![](images/300b/img117.png)

![](images/300b/img117_1.png)

**1.18** Now go back to Main page and click on **Actions** Tab this time.Select **Return** Item as shown below

![](images/300b/img118.PNG)

**1.19** Next drag and drop selected Item on the same swimlane. Since we are alredy set up map previously (1.14), delet the newly appered one.

![](images/300b/img119_1.PNG)

Your overall setup should look like this.This completes our one - **if else** logic

![](images/300b/img119.PNG)

**1.20** Next go to the **Invoke** tab and select **Rest** connector - `OnlineShoppingPaymentInvoke` as shown below 

![](images/300b/img120.png)

**1.21** Drag and drop connector to **Otherwise** swimlane as shown below

![](images/300b/img121.png)

**1.22** A new page will come up. Provide the below details as marked in red. Once done, click **Next**.

![](images/300b/img122.png)

**1.23** Here we need to add two input fields for request mapping. Click on **+** button and add  parameters as shown below.Click **Next** once done.

![](images/300b/img123.png)

**1.24** This is section where we need to select Response mapping. Select **JSON Sample** and click **Inline** section as marked in red

![](images/300b/img124.png)

**1.25** A blank textbox opens up.Enter a Sample Jason as shown below.Click **OK** once done.

![](images/300b/img125.png)

**1.26** Click **Next**

![](images/300b/img126.png)

**1.27** This is final step of adapter configuration.Check all the parameters and click **Done** to exit from here.

![](images/300b/img127.png)

**1.28** Now we are back to Integration page.Here you will see two new Items as shown

![](images/300b/img128.png)

**1.29** Click on **Edit** button for the mapper file as shown 

![](images/300b/img129.png)

**1.30** A new page opens up.Update the PaymentAction field with expression value as shown. Also map **OrderId** from source with target.Once done Next Click  **Validate** to verify all the parameters.Finally select **Close** to exit from this page. 

![](images/300b/img130.png)

![](images/300b/img130_1.png)

**1.31** Now we are back to the Inegration Page,from here select **Return** action item as shown

![](images/300b/img131.png)

**1.32** Drag and drop to the same swimlane,your entire message flow should look like this
![](images/300b/img132.png)

**1.33** Next click on **Edit** button for response mapping as shown

![](images/300b/img133.png)

**1.34** A new mapper page shows up.Update the response parameters and Click **Validate** to update the same.Once done click **Close** to exit the same.

![](images/300b/img134.png)

![](images/300b/img134_1.png)

**1.35** Click on **Save** and then **Close** to exit the integration design canvas

![](images/200/image045.png)

You should see your _New_ integration in list of _Integrations_

![](images/300b/img143.png)

**1.36** Click on the switch next to your integration to activate

![](images/200/image047.png)

**1.37** On the **Activate Integration ?** popup window, select **Enable Tracing**, then **Include payload**, then click on **Activate**

![](images/300b/img144.png)

![](images/300b/img145.png)

**1.38** Once your integration is activated, select Cogwheel type of button (1.) and select the givem url.

![](images/300b/img145_1.png)

**1.39** You will be redirected to a new page. Coppy Endpoint URL and save it for later. You are going to use it in Postman for testing your request.

![](images/300b/img145_2.png)

### Testing your Integrations

Testing the activated integration can be done using multiple tools and depends on your preference. See each relevant product's website on how to install the tool, if its required.

**1.1** Got to URL **chrome:/apps** in _Chrome_ and open POSTMAN

![](images/200/image066.png)

**1.2** Click on the Collection tab as shown below  

![](images/300b/img146.png)

Provide the name for your collection as it shown below

![](images/300b/img146_1.png)

Click on the AddRequest tab as shown below

![](images/300b/img146_2.png)



**1.3** Here provide the name of the Integration and optional description and click **Save**

![](images/300b/img147.png)

**1.4**A new page comes up.Click on **Authorization Tab**. For Authorization type, select Basic Auth. Provode the credentials that you used to sign in to Oracle Cloud.

![](images/300b/img148.png)

**1.5** Next we need to set the request. 1. Select POST method and copy paste the Endpoint URL that you saved earlier (from 1.39). 2. Click on **Body** section and update the request json as shown below 

```json
{"OrderId": "1235", "UnitPrice": "10000", "NumberOfItems": "3", "ShippingState": "OH", "Model": "WalkeyTalkey 1.0", "ReturnReason": "Does Not Work"}
```

Make sure you select JSAN(applicatiom/json) format (5)

![](images/300b/img148_1.png)

**1.6** Click on Send Button and check the response at bottom.

![](images/300b/img150.png)

![](images/300b/img137.png)

**1.7**Now go back to the Integration Page  and navigate  **Tracking** field as shown below 

![](images/300b/img152.png)

![](images/300b/img152_1.png)

![](images/300b/img152_2.png)

**1.8** Click on the order instances as shown

![](images/300b/img153_1.png)

**1.9** You will see the overall flow  of the integration as shown 

![](images/300b/img154_1.png)


```
You have now completed Lab 300b of the OIC Developer Workshop. In the next lab, we are going to create a User Interface using Visual Builder Cloud Service (VBCS), then call the REST API with online shopping request.

- This Lab is now completed.