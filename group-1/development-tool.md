---
description: 平常开发中使用到的
---

# 🔧 development tool

### apollo

统一获取apollo配置

```go
// get apollo config
recommendDegradeConfig := &model.RecommendDegradeConfig{}
_ = bizcommon.GetApolloJsonConf(model.DevelopmentRecommendDegrade, recommendDegradeConfig)

```



### time

获取当天开始、当前、当天结束时间戳

```
beginTimeNum, currentTime, endTimeNum := bizcommon.GetDayTimestamp()
```



### 接口返回校验

```
err = bizcommon.CommonRespCheck(resp, err)
```

