# OIC (ICS) Developer Workshop

![](images/j2c-logo.png)

> Updated: July 13th, 2018

## Journey To The Cloud: Oracle Integration Cloud (OIC) - Enterprise Integration Hands On Lab
A hands-on workshop to dive into development on Oracle's Integration Cloud Platform

## Overview
Enterprises can innovate faster, improve customer engagement, drive business-process efficiency, and accelerate digital transformation with Oracle Cloud. Oracle is the enterprise technology partner that positions companies for tomorrow, today; empowering businesses of all sizes on their journey of digital transformation. Oracle Cloud provides leading-edge capabilities in software as a service, platform as a service, infrastructure as a service, and data as a service.

At Oracle we have invested in delivering a plethora of new Cloud Services and we want to show you how simple – yet powerful they are. We specifically wanted to focus on low code, high productivity services that can be used in building enterprise grade solutions. We believe the best way to do this is to showcase a real world business solution comprised of these services. You will build the entire solution during the course of this workshop all in a stress-free fun environment. 

This workshop will focus on the Integration Cloud Service (ICS) capabilities within Oracle Integration Cloud (OIC).  Oracle ICS delivers best in class “Hybrid” Integration. ICS is a simple and powerful integration platform in the cloud to maximize the value of your investments in SaaS and on-premises applications. 

It includes an intuitive web based integration designer for point and click integration between applications and a rich monitoring dashboard that provides real-time insight into the transactions, all running on a mature runtime platform on Oracle Public Cloud. ICS will help accelerate integration projects and significantly shorten the time-to-market through it's intuitive and simplified designer, an intelligent data mapper, and a library of adapters to connect to various applications.

## About OIC:

Oracle Integration Cloud (OIC) brings together all the critical capabilities of a complete Application Integration, Process Automation, Visual Application Building and Integration Analytics solution into a single unified cloud service. Oracle Integration Cloud now brings real-time and batch based integration, structured and unstructured processes, case management, stream analytics, zero code integration insight etc, allowing customers to service all their end to end integration needs in one cohesive platform so that all users can now transition and collaborate across these capabilities and projects seamlessly.

![](images/oic.png)

### Oracle Integration Cloud Features

- Integrate Applications - Deliver integrations up to 6X faster with pre-built adapters for your SaaS and on-premises systems.

- Automate Processes - Streamline your digital workforce with an easy, visual, low-code process automation platform that simplifies day to day tasks by getting employees, customers, and partners the services they need to work anywhere, anytime, and on any device.

- Build Applications Visually - Rapidly create and host engaging business applications with a visual development environment right from the comfort of your browser. Define business objects, integrate data from external system, incorporate business processes, and design tailored interfaces to create your apps.

- Gain Insight - Gain real-time insight into end-to-end processes with guidance on best next steps for your business operational excellence and run massively parallel real-time analytics on streaming data for instant actionable insights. 

## Hands-on Lab Overview
This hands-on lab will allow participants to do the following:
- Lab 100 - Explore Oracle Integration Cloud Service
- Lab 200 - Create a simple Hello World API echo service
- Lab 300 - Create an API to retrieve enterprise information from an On-Premise Oracle Database using OIC Connectivity Agent
- Lab 400 - Implement an Order API to create Orders in an On-Premise Enterprise Application (Oracle EBusiness Suite)

The ICS integration that we'll be working with is shown in the following picture:

![](images/overview-image.png)

Here is a description of what is happening with this integration:

SoapUI will be used to test the exposed Web Service endpoint of the ICS integration called *UserXX Create EBS Order* (where XX will be the Number assigned by the Instructor).  This integration has 3 connections.  The incoming message is received by the incoming *UserXX SOAP* Soap Connection.  The *UserXX Create EBS Order* orchestration makes 1 query into the database using the *UserXX Oracle DB 12c* connection to get details needed to create an order.  The orchestration finally uses the *UserXX EBS OPERATIONS* EBS Adapter connection for creating the order in EBS.  After the order is created in EBS, the Order Number is returned to the calling web service.

## Get Started: 
Open the navigation menu using the hamburger icon in the upper left of the menu bar to choose a lab guide and get started.

The hamburger menu has an icon that looks like this: <img src="images/menu.svg">



## LAB 100 - Explore OIC Integration Cloud Service


## OIC Login

Open  your OIC Enviorment as shared,your login page looks like this.Provide your username and password and click 'Sign In'. 

![](images/OICS_Env.PNG)


## OIC Connection

You will now be presented with the OIC Service Console from which you will be performing the rest of this workshop lab.

![](images/OIC_HOME.PNG)



## Explore OIC Connection

Select **Integrations** Tab,then followed by Connections tab from designer page  as shown below- 

![](images/OIC_INTEGRATION_TAB.PNG)

![](images/OIC_INTEGRATIONS_CONNECTIONS_TAB.PNG)



Make note of the connections that have been created

![](images/OIC_INTEGRATIONS_PAGE.PNG)


Click on the **Create** button in the upper-right so we can see all the different  Connectors that are available.

![](images/OIC_CONNECTIONS_CREATE.PNG)


Scroll through the list of connection types that are available in OIC:

![](images/OICS_ADAPTERS_LIST.PNG)

Note that the icons with the plug are those that support the OIC Connectivity Agent for those service types which are not in the cloud, but on-premise, behind the company firewall.


When you are done browsing, select the “Cancel” button to dismiss the “Select an Adapter” dialog.


## Explore OIC Integrations

Select the **Integrations** from  menu selection

![](images/OIC_INTEGRATIONS_TAB.PNG)


Make note of the integrations that have been created.We will be working with the integration called Online Shopping App Payment Validation

![](images/OIC_ONLINE_SHOP_LAB.PNG)


 Open the integration Lab Online Shopping App Payment Validation by clicking on the integration name. We want to see what it looks like. Since the integration is already active, we’ll be looking at it in Viewing mode. There will be a warning that Edit is not possible...

 ![](images/OICS_ORCHESTRATION_WINDOW.PNG)

 You can see that this orchestration has many steps in it. The view of the orchestration is Zoom to Fit in the browser real estate. In order to get a closer view of the individual steps, you can either scroll with your mouse wheel to zoom in and out, or you can use the -/+ slider in the top right of the designer.

 Try zooming in and out by using both methods.

 Try selecting the Maximize viewing control on the very right of the view control bar. This will hide some of the detail on top of the screen to give the designer the most area to work in. Hitting the Maximize button again will toggle that view..

 ![](images/OIC_INTEGRATION_MAXIMIZE_TAB.PNG)

 The component at the very top of the orchestration is the **Trigger**. The trigger is representative of the connector that’s sending data into the integration. It is highlighted with a little lightning bolt signifying an incoming event.

 If you hover over the **Trigger** node, you can see the details. Our trigger is a REST connector type. It is called ProcessPayment. 

 ![](images/OIC_TRIGGER_REST_ENDPOINT.PNG)

If you click on the Trigger, a pop-up will appear with a view icon in the shape of an eye. Select the little eye so we can walk through the wizard that was used to setup the REST trigger

![](images/OIC_EYE_ORCHESTRATION.PNG)

After the wizard initializes, you’ll be shown the basic information about the trigger – it’s name and description.

![](images/OIC_REST_ENDPOINT_BASIC_INFO.PNG)


Select the **Next** trigger button you will able to see request parameters.

![](images/OIC_REST_REQUEST_PARAMETERS.PNG)

Select **Next** you will be able to see CORS configuration.

![](images/OIC_REST_CORS.PNG)

Finally Select Summary tab to see Trigger’s configuration.

![](images/Capture_REST_SUMMARY.PNG)

Select the **Close** button to dismiss the Trigger view wizard.

Let’s view the next node down in the integration. This is an Assign node. The job of this Assign activity is to initialize variables that will be used in the calls to be made

![](images/OIC_ASSIGN_VRBL.PNG)

The variables defined in this Assign activity are view only. Later on in this lab,we’ll de-activate the integration and all the values will be changeable.

![](images/OIC_ASSIGN_VRBL_DATA.PNG)

Pan down to the map called Map To ProcessPay. Click on this map activity and select the view icon

![](images/OIC_MAPPING.png)


What you’ll see in the mapper is the possible input variables on the left and the execute Response that can be mapped to on the right. The values that have been mapped are shown to the right  in the mapper.Click close to close the mapper.Finally close the integration.


![](images/OICS_MAPPING.png)



## Explore OIC Agents

Select the **Agents** menu selection

![](images/OIC_AGENTS.png)

Make note of the agent that has been created to communicate 

![](images/OIC_AGENT_SELECTION.PNG)

The Connectivity Agent is available from the Download pull-down on the Agent page shown below:

![](images/OIC_CONN_AGENT_DOWN.PNG)


### Explore OIC Monitoring Console

Select the **Designer** menu selection at the top to go back to the main left-hand navigation menu level.


![](images/OICS_MONITORING_BACK_BUTTON.png)

Next, select the **Monitoring** menu selection to go the OIC monitoring capabilities.

![](images/OIC_MONITORING1_TAB.png)


Next, select the **Dashboards** selection to go to the main ICS monitoring dashboard page.

![](images/OIC_DASHBOARD.png)

You will be presented with the ICS Monitoring Dashboard. Observe the various data that is available from this dashboard such as % of successful messages, # of Currently Used Connections, etc.

![](images/OIC_DASHBOARD_HEALTH.PNG)

On the right side of the Dashboard there are links where you can view the **Activity Stream**,Download the logs, and Download an Incident if a service request needs to be raised.Click on the Activity Stream link.


![](images/OIC_ACTIVITY_STREAM.png)

You will be directed to the Integration screen where you can view a summary of all messages that have passed through ICS in a tabular form.


![](images/Capture_MONITOR_INTEGRATIONS.PNG)


In the Activity Stream you can see the steps in the  integration that were executed and whether or not they were successful.

## Explore OIC Monitoring Console - Logfiles

 In order to see the details of the payload that passed through the ICS integration, you need to download the Log from the Download Logs link on the right of the Activity Stream.

 ![](images/ORACLE_DIANOSTIC_LOGS.png)

 Select the **Download Diagonastic** link and then save the zipfile to a location on your workstation such as C:\temp (Windows path)

 ![](images/Capture_download_logs.PNG)


 Extract the zipfile and you’ll see that there are 2 directories of logfiles – this is because the ICS instance is running on a cluster of 2 servers for high availability.

 ![](images/OIC_HYBRID_SERVER.PNG)

 Navigate into one of the server directories and examine the ics-flow.log file in your favorite text editor.

 Here is a view of the end of the ics-flow.log file in the Notepad++ text editor :

 ![](images/Capture_OICS_Log.PNG)

 This logfile is helpful for investigation during development or runtime analysis. The capture of the runtime payloads can be turned on or off during activation of the ICS integration where you are prompted whether or not you want to save the payloads.


 ## Explore ICS Monitoring Console - Integrations

 Back in the OIC Monitoring console, select **Integrations** from the left-hand navigation.

 Note that all the statistics that are shown.


![](images/OIC_MONITORING_INTEGRATIONS.png)



## Explore ICS Monitoring Console - Tracking


Select the **Tracking** link in the navigation bar on the left


![](images/OIC_Tracking.png)

The ICS Tracking monitor page shows all integration flows that have been executed.


Select the chevron just to the right of the Tracking label at the top of the page to change the granularity of the Tracking report to Last 1day 

![](images/OIC_Retention.png)

Next, drill into a completed integration flow by selecting the integration name.

![](images/OIC_Integration_Name.png)

 We can now see that all steps in the this OIC integration flow were successful because the arrow is green highlighting all the orchestration flow steps

 ![](images/OICS_Flow.PNG)



 Select the **Close button** to go back to the OIC monitoring page.

 ![](images/OICS_Close.png)


 We are now done exploring the OIC monitoring features.


 This OICS Overview Lab is now completed.






























