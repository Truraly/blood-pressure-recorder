# 血压健康记录工具

express + Vue + ElementUI + Echarts 的血压健康记录工具

## TODO

- [ ] 添加记录吃饭，睡觉时间的功能
- [ ] 重新构建突变渲染的逻辑和展示
- [ ] 完善修改数据的功能
- [ ] 添加更多视图
- [ ] 参考资料构建更合适的功能
- [ ] 考虑使用 SQLite 存储数据

## 功能设计

血压记录，查看

- 便捷的记录血压数据
- 查看血压数据

血压信息包括

- 高压
- 低压
- 心率
- 时间
- 备注
- 位置

  - 右手（default）
  - 左手
  - 其他

- 自动对相距 10 分钟内的数据进行平均值计算
- 忽略心率>85 的数据

- 查看 1 日，3 日，7 日内平均血压数据
- 以日为单位查看平均血压数据
- 以周为单位查看平均血压数据
- 以月为单位查看平均血压数据
- 以年为单位查看平均血压数据

**考虑展示各个时间段的血压信息**

目标静坐舒张压 <130mmHg，收缩压 <80mmHg

- 输入血压，修改血压记录，删除血压记录
- 查询血压记录

由一个定期维护的 json 文件来维护数据

```json
{
  "records": [
    {
      "high": 120,
      "low": 80,
      "heartRate": 60,
      "time": 1620000000,
      "remark": "早上测量",
      "location": "right"
    },
    {
      "high": 120,
      "low": 80,
      "heartRate": 60,
      "time": 1620000100,
      "remark": "晚上测量",
      "location": "right"
    }
  ]
}
```

- 主页
  - 今日平均最高血压/最低血压/心率 距离目标的差值
  - 近 3 日平均最高血压/最低血压/心率 距离目标的差值
  - 近 7 日平均最高血压/最低血压/心率 距离目标的差值
  - 快速记录血压
  - 最近的 x 条记录
- 记录列表，可以按时间查看记录，可以修改/删除记录，依据为 timestamp
- 趋势图，以日，3 日，7 日，月，年为单位查看平均血压数据

接口：

- 新增血压记录
- 获取某 timestamp 之后的血压记录
- 获取前 x 条血压记录
- 修改血压记录
- 删除血压记录

## 参考资料

- 建议每天早、晚各测量 1 次血压；每次测量至少连续获取 2 次血压读数，每次读数间隔 1~2 min，取 2 次读数的平均值，若第 1、2 次血压读数的差值>10 mmHg，则建议测量第 3 次，取后 2 次读数平均值；测量血压前 30 min 避免剧烈运动、饮酒、喝含咖啡因的饮料以及吸烟；在每次测量之前，安静休息 3~5 min（1D）
- 推荐早上在服药前、早餐前、排空膀胱后测量血压（1B）。
- 建议晚上在晚餐前测量血压，条件不允许时建议在睡前 1 h 内测量（2D）。
- 初诊或血压未控制的患者，推荐每周至少连续 3 d 进行 HBPM（1B）。
- 血压控制良好的患者，建议每周进行 1~2 d 的 HBPM（2D）。

2017 年的一项系统评价对影响血压测量误差
的因素进行了分析，在 29 个潜在影响因素中，有
8 个因素与患者相关，包括测血压前急性进餐、饮
酒、饮用咖啡、吸烟、膀胱扩张以及休息时间不足
等，这些因素可导致低估或高估患者的“真实”静息
血压［49］
。一项横断面研究比较了晚餐前和就寝时
HBPM 的差异，结果显示晚餐前测得的血压值与早
上的血压值相关性最好，沐浴后 2 h 内和饮酒后 8 h
内测得的血压值明显降低［71］
。因此晚上的血压测
量应主要考虑患者的夜间活动，有条件者应在晚餐
前测量，若不可行，则建议在睡觉以及沐浴前测量。
如患者晚上需服用降压药物，则建议在服药前测量
血压

高血压患者的非药物干预措施

| 方式             | 干预内容                                                                                                                                                                                                                                                          |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 饮食干预         | DASH：坚持服用富含水果、蔬菜、全谷物和低钠低脂乳制品<br/>食用替代盐或低钠富含钾饮食：使用替代盐烹饪或食用替代盐食品；建议钠盐的摄入<5 g/d（约 1 茶勺），最佳目标是<1.5 g/d，推荐钾的摄入量 3 500~4 700 mg/d                                                       |
| 运动干预         | 中等强度有氧运动：30~60 min/d、5~7 d/周，达到最大心率的 50%~70%<br/>抗阻力量练习：90~150 min/周，一次性最大负荷的 50%~80% 的重量，6 个练习/组，进行 3 组，重复 10 次<br/>等距握力训练：每次 2 min，共 4 次，每次间隔 1 min，每周 3 d<br/>太极和气功也可以协助降压 |
| 减压干预         | 呼吸控制：每日睡前进行缓慢有规律的呼吸（最好借助专业的呼吸设备），目标呼吸频率<10 次/min，15 min/次，每周>40 min<br/>冥想：每次 20 min，2 次/d<br/>瑜伽：每周 3 d，每天至少 30 min                                                                                |
| 减重干预         | 限制每日热量 ≤500~750 kcal<br/>运动方式选择中到高强度的有氧运动，每天 30~60 min，5~7 d/周，达到最大心率的 60%~90%<br/>最佳目标是达到理想体重，体重指数 18.5~23.9 kg/m 2，控制腰围至男性<90 cm，女性<80 cm                                                         |
| 戒烟限酒         | 不吸烟、彻底戒烟、避免被动吸烟<br/>饮酒者降低酒精摄入：男性 ≤20 g/d，女性 ≤10 g/d，最好戒酒，避免酗酒                                                                                                                                                             |
| 综合生活方式干预 | 饮食和运动联合干预是最有效的非药物干预措施，与其他生活方式干预措施同时进行可最大程度地降低血压                                                                                                                                                                    |

运动项目可选择骑车、游泳、健步走、跑步、羽毛球、乒乓球、健身操、团体类运动等有氧运动项目，以及哑铃、小沙袋和弹力带等抗阻力量练习，需注意避免低头和憋气的动作。