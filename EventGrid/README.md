# React to Critical Device Lifecycle Events and Trigger Actions

![Header Image](images/eventgrid.jpg)

Azure IoT Hub integrates with Azure Event Grid so that you can send event notifications to other services and trigger downstream processes. Configure your business applications to listen for IoT Hub events so that you can react to critical events in a reliable, scalable, and secure manner. For example, build an application to perform multiple actions like updating a database, creating a ticket, and delivering an email notification every time a new IoT device is registered to your IoT hub.

<iframe src="https://channel9.msdn.com/Shows/Internet-of-Things-Show/Azure-IoT-Hub-Integration-with-Azure-Event-Grid/player" width="480" height="270" allowFullScreen frameBorder="0"></iframe>

In this lab you will learn how to

* Create logic app to be able to send email notifications

* Create Event Grid

* Connect IoT Hub to Event Grid

## Create Logic App

Create a Logic App to be able to send email notifications

Click on **Create a resource**

![Create Resource](images/create_resource.png)

Click on **Enterprise Integration**

![Enterprise Integration](images/enterprise_integration.png)

Click on **Logic Apps**

![Create Logic App](images/logic_app.png)

Use existing resource group created in previous steps and press Create

![Create Logic App](images/02_Create_LogicApp_Submit.png)

Using Logic App Designer, Create New App

![Create App](images/03_Logic_App_designer.png)

Select HTTP Request

![Select HTTP Request](images/04_Http_Request.png)

Provide a Sample Payload

```code
[{
  "id": "56afc886-767b-d359-d59e-0da7877166b2",
  "topic": "/SUBSCRIPTIONS/<Subscription ID>/RESOURCEGROUPS/<Resource group name>/PROVIDERS/MICROSOFT.DEVICES/IOTHUBS/<IoT hub name>",
  "subject": "devices/LogicAppTestDevice",
  "eventType": "Microsoft.Devices.DeviceCreated",
  "eventTime": "2018-01-02T19:17:44.4383997Z",
  "data": {
    "twin": {
      "deviceId": "LogicAppTestDevice",
      "etag": "AAAAAAAAAAE=",
      "status": "enabled",
      "statusUpdateTime": "0001-01-01T00:00:00",
      "connectionState": "Disconnected",
      "lastActivityTime": "0001-01-01T00:00:00",
      "cloudToDeviceMessageCount": 0,
      "authenticationType": "sas",
      "x509Thumbprint": {
        "primaryThumbprint": null,
        "secondaryThumbprint": null
      },
      "version": 2,
      "properties": {
        "desired": {
          "$metadata": {
            "$lastUpdated": "2018-01-02T19:17:44.4383997Z"
          },
          "$version": 1
        },
        "reported": {
          "$metadata": {
            "$lastUpdated": "2018-01-02T19:17:44.4383997Z"
          },
          "$version": 1
        }
      }
    },
    "hubName": "egtesthub1",
    "deviceId": "LogicAppTestDevice",
    "operationTimestamp": "2018-01-02T19:17:44.4383997Z",
    "opType": "DeviceCreated"
  },
  "dataVersion": "",
  "metadataVersion": "1"
}]
```

![Provide Sample Payload](images/05_Sample_Payload.png)

## Setup Notification by Sending Email 

Click on New Step

![New Step](images/06_New_Step.png)

Add an action

![Add an Action](images/07_Add_new_Action.png)

Choose Mail

![Choose Mail](images/08_Choose_Mail.png)

Finish Mail Actions

![Finish Mail Actions](images/09_send_email.png)

Sign in to email

![Sign in to email](images/10_signin_to_email.png)

Create Email template

![Create email template](images/11_Send_Email.png)

## Copy Request URL

![Copy Request URL](images/12_eventurl.png)

## Integrate With IoTHub

Integrate Logic App with IoTHub via Event Grid

![Imported Script](images/13_IoTHub_EventHub.png "Integrated with IoTHub")

Click on Event Subscription

![Integrated with IoTHub](images/14_empty_event_subscription.png)

Copy the URL from previous steps into Subscriber Endpoint and click create

![Integrated with IoTHub](images/15_device_events.png)

## Add Device and Test Notification

Go To IoTHub -> IoT Devices (Device Management) -> Add

![Add Device](images/16_add_device.png)

Click Save button to create a new device

![Add Device](images/17_add_device.png)

You Should get an email notification

![Email Notification](images/18_email_generated.png)

## Delete Device and Test Notification

Go To IoTHub -> IoT Devices (Device Management) -> Select Device you created in previous step -> Delete

![Delete Device](images/19_delete_device.png)

You Should get an email notification

![Email Notification](images/20_email_generated.png)
