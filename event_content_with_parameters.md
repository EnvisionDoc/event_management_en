# 告警内容显示流式计算当中的参数

## 背景

​针对计算点告警，部分开发者希望告警内容当中不单单只显示固定的文本，还希望可以显示计算过程当中产生的参数遍历。本文主要讲解内容的配置规范，以及流式计算当中的参数设置规范。

## 告警内容配置方法

​如果告警内容当中希望使用参数，需要使用“%参数名%”来引用参数。

​以光伏领域为例，汇流箱离散率异常是最常见的告警信息。假设汇流箱离散率状态计算点名为：CBX.BranchState。CBX.BranchState=1代表离散率异常，CBX.BranchState=0代表离散率正常。在离散率告警内容当中，用户希望不仅能够知道哪台设备出现离散率异常，还希望知道出现离散率异常时，知道众多支路当中的最大支路，最大支路电流，最小支路，最小支路电流，中位数支路，中位数支路电流。则汇流箱离散率异常的告警内容配置如下：

```
离散率>10%超过15分钟，最低支路：%MIN_BRANCH%,%MIN_BRANCH_VALUE%A，中位数支路：%MID_BRANCH%,%MID_BRANCH_VALUE%A，最高支路：%MAX_BRANCH%,%MAX_BRANCH_VALUE%A
```

​	这个带参数的告警内容，使用到的参数如下：

- MIN_BRANCH

- MIN_BRANCH_VALUE

- MID_BRANCH

- MID_BRANCH_VALUE

- MAX_BRANCH

- MAX_BRANCH_VALUE

  除去“%参数名%”，其他内容由用户自定义。



## 流式计算针对用于告警显示参数的开发规范

​流式计算开发可以参考开发者平台上提供的流式计算服务开发文档。针对告警内容需要显示的参数信息，需要对计算点做特殊处理。例如前面提到的离散率状态计算点CBX.BranchState，需要将对应的参数写入到计算点的attribute当中。

### 代码示例

```java
package com.envision.energy.calculate.app;

import com.envision.energy.sdk.eos.calculate.data.DeviceCal;
import com.envision.energy.sdk.eos.calculate.data.IEosDataService;
import com.envision.energy.sdk.eos.calculate.data.PointCal;
import com.envision.energy.sdk.eos.calculate.data.SiteCal;
import com.envision.energy.sdk.eos.calculate.data.VirtualPoint;
import com.envision.energy.sdk.eos.calculate.data.*;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class CombinerCal {
    private static Logger logger = LoggerFactory.getLogger(CombinerCal.class);
    private static CombinerCal instance = new CombinerCal();

    public static CombinerCal getInstance() {
        return instance;
    }


    public List<VirtualPoint> calCbxBranchStateList(SiteCal site, IEosDataService handler) {
        List<VirtualPoint> result = new ArrayList();

        List<DeviceCal> deviceCalList = site.getDeviceListByDeviceType("207");
        if ((deviceCalList != null) && (!deviceCalList.isEmpty())) {
            for (DeviceCal dc : deviceCalList) {
                VirtualPoint branchStatePoint = calBranchState(dc, "CBX.Cur", "CBX.BranchState");
                if (branchStatePoint != null) {
                    result.add(branchStatePoint);
                }
            }
        }
        logger.info("calCbxBranchStateList return data result size:[{}]", Integer.valueOf(result.size()));
        return result;
    }

    public VirtualPoint calBranchState(DeviceCal device, String curPointId,  String pointId) {
        PointCal curCal = device.getPoint(curPointId);

        String value = "0";
        long current = site.getCalSysTime();
        Map<String, String> attr = new HashMap();
        if (curCal != null) {

            value = "1";
            String maxValue = "4";
            String maxBranch = "1";
            String minValue = "1";
            String minBranch = "4";
            String midValue = "2";
            String midBranch = "6";

            String infoKeys = "";
            if (maxBranch != null) {
                infoKeys = infoKeys.concat("MAX_BRANCH").concat(",");
                attr.put("MAX_BRANCH", maxBranch);
            }
            if (maxValue != null) {
                infoKeys = infoKeys.concat("MAX_BRANCH_VALUE").concat(",");
                attr.put("MAX_BRANCH_VALUE", String.format("%.1f", new Object[]{maxValue}));
            }
            if (minBranch != null) {
                infoKeys = infoKeys.concat("MIN_BRANCH").concat(",");
                attr.put("MIN_BRANCH", minBranch);
            }
            if (minValue != null) {
                infoKeys = infoKeys.concat("MIN_BRANCH_VALUE").concat(",");
                attr.put("MIN_BRANCH_VALUE", String.format("%.1f", new Object[]{minValue}));
            }
            if (midBranch != null) {
                infoKeys = infoKeys.concat("MID_BRANCH").concat(",");
                attr.put("MID_BRANCH", midBranch);
            }
            if (midValue != null) {
                infoKeys = infoKeys.concat("MID_BRANCH_VALUE").concat(",");
                attr.put("MID_BRANCH_VALUE", String.format("%.1f", new Object[]{midValue}));
            }

            if (infoKeys.length() > 0) {  //重要且必须，组装infoKey
                infoKeys = infoKeys.substring(0, infoKeys.length() - 1);
                attr.put("infoKeys", infoKeys);
            }
        }
        VirtualPoint result = new VirtualPoint(pointId, value, current, attr);
        result.setDeviceID(device.getDeviceID()); //重要且必须，将虚拟点绑定到具体的device上
        return result;
    }
}
```

**注意** infoKey为必须项，告警内容通过infoKey实现识别出具体有哪些告警参数需要显示到告警内容当中。

​上述示例代码组装的attributes内容如下：

```json
{
    "infoKeys": "MAX_BRANCH,MAX_BRANCH_VALUE,MIN_BRANCH,MIN_BRANCH_VALUE",
    "MAX_BRANCH": "1",
    "MAX_BRANCH_VALUE": "4",
    "MIN_BRANCH": "4",
    "MIN_BRANCH_VALUE": "1",
    "MID_BRANCH": "6",
    "MID_BRANCH_VALUE": "2"
}
```

​用户可以通过eeop/domainService/getmdmidspoints接口获取测点信息验证attributes是否正确设置。如下图所示：

![1](../PIC/20180628-01.png)

![1](../PIC/20180628-02.png)
