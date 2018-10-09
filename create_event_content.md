# Creating event contents

To define contents for an event, you'll provide the event ID, description, event type and sub, device type, and the causes and resolutions for the event.

## Before you start

Define the event groups that you'll need to select from when defining the event content. For more information, see [Creating event groups](create_event_group.md).

##

定义事件的具体内容，主要包括**事件ID**，**描述**，**事件类型**，**设备类型**四个部分，**事件类型** 需要和事件分组中的类型ID进行关联，设备类型通常指这个事件来自什么类型的设备。事件内容定义除了以上四个必要属性外，还可以对每一个事件定义其产生的原因和可能的解决方案。

告警内容的定义过程如下：

1. 选择“内容定义”菜单；

在事件管理菜单中选择“内容定义”，然后选中对应的领域：风电

![1](/media/2018-1-12 18-20-01.png)

2. 添加告警内容

点击**添加告警**内容后，出现如下画面，在其中填入：

![1](/media/2018-1-12 18-20-39.png)

- 告警ID：

o   告警ID需要自己进行编码，风机状态点的每一个值需要进行一个编码，作为一条告警，如上表中的风机状态有1,2,3,4,5总共5个值，则每一个值需要定义一条告警内容，编码ID最好能区别出不同的设备型号，因为风机类型A和风机类型B的风机状态相同的值会具有不同含义的。

o   建议编码示例：GS_ST_001,其中前两位为机型（或厂家）编码，中间表示风机状态，后面三位表示风机状态的值；

- 告警类型/告警子类型：

o   告警类型和子类型直接选择系统之前已经定义好的告警类型即可；

o   每一条告警内容应该对应什么告警类型和子类型，需要领域业务方根据业务需求线下定义好；

- 告警内容描述：

o   定义告警输出的内容，本示例即对应风机状态点的描述；

- 领域设备：

o   选择生成该告警的设备，当前示例选择风机即可

- 原因及方案：

o   定义告警内容的时候，还可以对每一条告警内容定义告警产生的原因和对应的解决方案，可以直接文本输入，时非必填项。

【注意】：有多语言需求的，需要在英文环境下再输入一遍每一条告警内容的告警描述。
