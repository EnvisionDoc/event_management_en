# Creating event groups

According to the the type of the the events and priority that you must place to handle the events, define the event groups.

针对告警所属的分类和处理优先级，对定义告警的类型与等级。

For an event type, you can define sub-types according to your needs. After you enter the event type and severity name, EnOS automatically assigns type ID and severity ID.

定义事件的等级和类型，每一种类型下面还可以定义不同的子类型。输入类型和等级定义的描述信息后，系统会自动生成对应的等级和类型ID。

The settings and description about the event groups supports globalization.

事件分组的描述支持国际化定义。

## Before you start

一般设备的告警类型与等级可以在设备说明书当中找到，当然也可以基于用户自身对设备的理解自定义类型与等级。例如，针对箱变温度超过85℃，存在潜在安全风险，因此告警类型定义为“EHS安全”，告警等级定义为警告。同时，因为这个告警是基于温度超过85℃定义的，也可以将其告警类型定义为“遥测越限”，具体归属于哪个类型与等级，由领域应用方决定。

For a specific domain device, the event types and severities definitions are typically found in its instructions; although you can customize the definitions according to your business needs too.

For example, a padmount transformer, potential security risks exist when the temperature exceeds 85 degree Centigrade. Therefore, the event type is EHS, and the severity is warining according to the device instructions. At the same time, before the event is defined based on the temperature threshold, you can also define it as an over-limit event, and set the type and severity according to the practices in the domain.

## Configuring event severity

1. 首先在事件管理的菜单中选中“**事件分组**”，并在页面上方选中需要配置的领域，如下图：

  ![1](/media/2018-1-12 18-09-34.png)

2. 点击页面中的“**添加告警级别**”，然后输入对应的告警等级的描述信息，系统会自动生成告警等级的ID，如下图，

  ![1](/media/2018-1-12 18-11-51.png)

**注意**:

- 告警等级主要用于告警的前端应用展示和历史告警分析，领域应用通过生成的告警等级ID（即：级别ID）识别各个告警等级；

- 告警等级支持多语言，在中文环境下输入的语言即为中文，切换到英文环境再次输入描述即为英文语言，其他语言也是一样的操作。

### 告警等级定义示例：

常规的一个告警等级定义如下所示：

| 告警等级ID | 英文描述 | 中文描述 |
| ---------- | -------- | -------- |
| 398000001  | Info     | 提示     |
| 398000002  | Warning  | 警告     |
| 398000003  | Fault    | 故障     |

告警等级ID其实是一个被应用使用的key值，应用需要知道每一个key对应的含义。例如，在领域告警应用当中，前端“当前告警”界面默认只显示“警告”和“故障”等级的告警列表，“提示”等级告警默认不展示。其实就是在告警应用当中定义默认只展示告警等级ID为398000002和398000003的告警。

## Configuring event types

告警类型包括告警类型和子类型，需要先定义告警类型，每一个告警类型下还需要定义子类型



1. 定义告警类型

在菜单中点击“**添加告警类型**”，出现如下输入框：
  ![1](/media/2018-1-12 18-16-29.png)

其中告警类型的ID系统会自动生成，只需要输入告警类型的描述即可。

2. 定义告警子类型

在告警类型的右侧点击“**添加子类型**”按钮，弹出子类型的定义框：
  ![1](/media/2018-1-12 18-18-26.png)
系统会自动生成告警子类型的ID，输入子类型的描述即可。
