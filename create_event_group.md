# Creating event groups

This topic instructs how to create the event severity and event type/sub event type via Event Management GUI.

After you enter the event type and severity name, EnOS automatically assigns type ID and severity ID.

The settings and description about the event groups supports globalization, that is you can define different languages of event contents.

## Before you start

For a specific domain device, the event types and severities definitions are typically found in its instructions; although you can customize the definitions according to your business needs too.

For example, a padmount transformer, potential security risks exist when the temperature exceeds 85 degree Centigrade. Therefore, the event type is EHS, and the severity is warning according to the device instructions. At the same time, because the event is defined based on the temperature threshold, you can also define it as an over-limit event, and set the type and severity according to the practices in the domain.

## Configuring event severity

1. Click **Event Management > Event Groups** from the left navigation panel of the EnoS Console, and select the domain to configure event groups for.

2. Click **Add Severity Level** and provide the description for corresponding severity level. The severity ID will be automatically assigned by the system upon submit.

    ![configure severity](/media/create_severity_level_window.png)

The severity levels are mainly used for filtering the event messages on GUI and analyzing the historical events. The domain application identifies the severity of the event by the ID of the severity level.

### Example of severity level

The following table shows a typical list of severity levels:

<table>
  <tr>
    <th>Severity Level ID</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>398000001</td>
    <td>Info</td>
  </tr>
  <tr>
    <td>398000002</td>
    <td>Warning</td>
  </tr>
  <tr>
    <td>398000003</td>
    <td>Fault</td>
  </tr>
<table>

The severity level can be used as a key value in the application for a domain. The application needs to know the corresponding meaning of each severity level. For example, in your event application for a domain, you can set to display only the events with severity _Warning_ and _Fault_ in the GUI. This feature is achieved by setting to show events whose severity level ID is _398000002_ or _398000003_.

## Configuring event types

You can define types and subtypes to facilitate your event management. A event type can comprise several subtypes.

### Define event Type

1. Click **Event Management > Event Groups** from the left navigation panel of the EnoS Console.

2. Click **Add Type** in the domain where the event type belongs. The event type ID is assigned by the system.

  ![configue event types](/media/example_add_event.png)

### Define sub event type

Click the `add subtype` of the event type where the subtype belongs. The ID is assigned by the system.

![1](/media/create_subtype_window.png)
