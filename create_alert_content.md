# Creating alert content

This topic instructs how to create an alert content record. To define content for an alert, you will provide the alert content ID, description, device model, alert type and subtype.

## Before you start

Ensure the alert type that the alert content record belongs to is created. For more information, see [Creating alert types](create_alert_type).

## Procedure

1. Click **Asset Alert > Alert Content** from the left navigation panel of the EnoS Console.

2. Click **Add Content**, and provide the needed information for the alert content. 

   ![1](media/create_alert_content.png)

  - **Content ID**

    It is recommended to define a meaningful content ID to distinguish different types of the device.

    In the wind turbine example, you should create separate alerts for each DI value because the same DI value for different types of wind turbines can represent different state. Therefore, each DI value requires an event content record. You can name the event ID such as `GS_ST_001`, where:

    + `GS` represents the code of the device type or the branch.
    + `ST` represents the state of the device.
    + `001` represents the DI value of the device.

  - **Description**

    In the wind turbine example, the description of the alert can be the description of the DI value.

  - **Device Model**
    Select a device type from the list.

    In wind turbines example, the device type is _turbines_.   

- **Alert Type / Subtype**

  Select an alert type and subtype from the list according to the actual business needs.