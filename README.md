# Meraki-Webhook-alerts-in-SNOW
Steps to configure Meraki webhook alerts in ServiceNow using the Meraki ServiceGraph Connector application

This document details the steps required to configure sending Webhook alerts from Meraki Dashboard to the ServiceNow instance in the form of Incidents.
However, before configuring the webhook part it is necessary to configure & connect your Meraki organization  & API key to the ServiceNow instance. Please refer to the [guided developer documentation](https://developer.cisco.com/meraki/build/servicenow/service-graph-connector-for-meraki) to setup those steps.
> Note: After installing the ServiceGraph connector application for Meraki in your ServiceNow instance, open the application and complete the following steps as mentioned inside the "Setup" menu item
Task 1: Configure the connection
and Task 2: Configure system properties

![meraki_sgc_main_menu](https://github.com/user-attachments/assets/845c8466-ce37-4dc1-8306-cbebef411d2f)

Task 3 of the process is to Configure Incident creation from Device Alerts.
![Task_3_SGC_setup](https://github.com/user-attachments/assets/ea4ed8af-1272-42ef-9242-3993499c56ba)


## 1. Create a user for alert configuration

Below is an example of the user account setup:
Navigate to Organization > Users

![navigate_user](https://github.com/user-attachments/assets/e0abdbb8-cc70-4bac-b84e-83dd8db7c745)

Create a new user by adding the fields and click on Set password to configure the password for this newly created user. Click on `Update` to save the new configurations.

Note: 
1. Make sure Active and Web service access only fields are set to True. This is to restrict this account from being able to login directly into your ServiceNow instance.
2. Alert configuration requires a user record created containing the role of `x_caci_sg_meraki.user`. Click on `Edit` to add this role to this user.

![add_user_SGC](https://github.com/user-attachments/assets/3214740e-4fd2-49c7-89b1-e4d3c46cc5bd)

Save the user ID and password in a safe place. These credentials will be required to configure Webhook receiver details in the Meraki Dashboard.

## 2. Configure Webhook receiiver in Meraki Dashboard

In the Meraki Dashboard, navigate to Organization > API & Webhooks > Webhooks > Receivers
Add a new receiver with the following details:

* name: Any name that you want to give to your webhook receiver
* httpServer URL: https://venXXXX.service-now.com/api/x_caci_sg_meraki/sgmeraki_device_alerts (Replace venXXXX with your ServiceNow instance)
* sharedSecret: username:password (This is your user ID & password created in step 1 above)
* Template: select the built in template for ServiceNow

Click Save, and then click "send Test" to ensure the setup is right. You should see a "webhook test was successful!" message

## 3. Setting up MT webhook alerts
In order to create incidents in ServiceNow for any webhook alerts coming from MT sensors, In your Meraki Dashboard navigate to
Sensors > AlertProfiles
configure the alerting thresholds per your requirement, and add the newly configured ServiceNow webhook receiver in Notfication recipients

![MT_alert_profile](https://github.com/user-attachments/assets/db208207-bda0-4ec6-ae07-812fd5290f1b)


