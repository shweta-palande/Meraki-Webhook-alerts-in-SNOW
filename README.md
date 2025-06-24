# Meraki-Webhook-alerts-in-SNOW
Steps to configure Meraki webhook alerts in ServiceNow using the Meraki ServiceGraph Connector application

This document details the steps required to configure sending Webhook alerts from Meraki Dashboard to the ServiceNow instance in the form of Incidents.
However, before configuring the webhook part it is necessary to configure & connect your Meraki organization  & API key to the ServiceNow instance. Please refer to the [guided developer documentation](https://developer.cisco.com/meraki/build/servicenow/service-graph-connector-for-meraki) to setup those steps.
> Note: After installing the ServiceGraph connector application for Meraki in your ServiceNow instance, open the application and complete the following steps as mentioned inside the "Setup" menu item
Task 1: Configure the connection
and Task 2: Configure system properties

![meraki_sgc_main_menu](https://github.com/user-attachments/assets/845c8466-ce37-4dc1-8306-cbebef411d2f)

Task 3 of the process is to Configure Incident creation from Device Alerts
## 1. Create a user for alert configuration

Below is an example of the user account setup:
Navigate to Organization > Users

![navigate_user](https://github.com/user-attachments/assets/e0abdbb8-cc70-4bac-b84e-83dd8db7c745)

Create a new user by adding the fields and click on Set password to configure the password for this newly created user. Click on `Update` to save the new configurations.

Note: 
1. Make sure Active and Web service access only fields are set to True. This is to restrict this account from being able to login directly into your ServiceNow instance.
2. Alert configuration requires a user record created containing the role of `x_caci_sg_meraki.user`. Click on `Edit` to add this role to this user.

![add_user_SGC](https://github.com/user-attachments/assets/3214740e-4fd2-49c7-89b1-e4d3c46cc5bd)

