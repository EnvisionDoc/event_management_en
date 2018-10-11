# Example scenario

该场景案例将针对风机设备中风机状态这个测点，给出配置风机状态变化的告警实例，其他遥信变位，遥测越限等告警也可以参照如下的实例进行配置。

## Background

某一种风机机型的风机状态点上送的值及描述如下表：

| DI Value | Desc_EN      | 描述_中文 |
| -------- | ------------ | --------- |
| 1        | Shutdown     | 紧急停机  |
| 2        | Stop         | 停机      |
| 3        | Normal  stop | 正常停机  |
| 4        | Stand-by     | 待机      |
| 5        | Run          | 运行      |

现在需要配置告警规则，当风机状态点等于“1（或2,3,4,5）”时，触发告警“紧急停机（或停机，正常停机，待机，运行）”。

## Procedure
1. [Create event groups](create_event_group).
2. [Create event contents](create_event_content).
3. [Create triggering rules](create_event_rule).
