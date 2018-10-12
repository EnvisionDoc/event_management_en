# Creating event contents

This topic instructs how to create an event content record. To define contents for an event, you'll provide the event ID, description, event type and sub, device type, and the causes and resolutions for the event.

## Before you start

Ensure the event group that the event content record belongs to is created. For more information, see [Creating event groups](create_event_group).

## Procedure

1. Click **Event Management > Event Contents** from the left navigation panel of the EnoS Console.

2. Click **Add Event** in the domain where the event group belongs.

  ![1](/media/create_event_window.png)

  - **Event ID**

    It is recommended to define a meaningful event ID to distinguish the different type of the device.

    In the wind turbine example, you should create separate events for each DI value because the same DI value for different types of wind turbines can represent different state. Therefore, each DI value requires an event content record. You can name the event ID such as `GS_ST_001`, where:

    + `GS` represents the code of the device type or the branch.
    + `ST` represents the state of the device.
    + `001` represents the DI value of the device.

  - **Event Type / Sub Event Type**

    Select an event type from the list according to the actual business needs.

  - **Description**

    In the wind turbine example, the description of the event can be the description of the DI value.

  - **Device type**
  -
    Select a device type from the list.

    In wind turbines example, the device type is _turbines_.   

  - **Causes and Resolutions(Optional)**：
  
    Addition information in text format about the causes and resolution of this event.
