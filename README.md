# StepHeal-Loop**(ELAK-Physicalcare-therapy)**

> 一个面向青少年运动康复的**数据驱动闭环康复系统**，连接患者、治疗师与客观健康数据，通过游戏化激励和临床决策支持，提升家庭康复训练的依从性与效果。

---

## **📖 项目简介**

**StepHeal-Loop**（仓库名：`ELAK-Physicalcare-therapy`）是一个开源的康复管理平台。它旨在解决传统康复中患者居家训练依从性低、医生缺乏客观数据、康复进展难以量化等问题。

系统通过收集患者的**步态、足底压力、活动能量、心率变异性**等客观数据，生成趋势报告，辅助治疗师制定个性化康复计划；同时利用**游戏化姿态追踪**激励患者完成每日训练，形成“评估—训练—反馈—调整”的闭环。

---

## **✨ 核心功能**

### **1. 患者端（Patient）**

- **每日康复计划**：查看治疗师分配的居家训练动作、目标次数与组数。
- **游戏化训练**：通过姿态追踪或计时器完成动作，获得积分、徽章与进度反馈。
- **症状与状态记录**：记录疼痛评分（VAS）、疲劳度、睡眠、用药情况。
- **数据同步**：自动上传 Apple Watch 等设备的活动能量、锻炼分钟、心率等数据。
- **时间表视图**：展示每日时间线，包括起床、上学、训练、用餐、睡眠等，并标记训练完成情况。



### **2. 治疗师端（Therapist）**

- **患者仪表板**：查看所有患者的康复轨迹、依从性、疼痛趋势、步态对称性等。
- **趋势报告**：基于步态不对称、足底压力、活动数据生成可视化图表。
- **处方管理**：为每位患者开具药物处方，并记录会诊笔记。
- **排班与预约**：查看每日会诊安排，每个时段可填写对应处方。
- **风险预警**：识别依从性下降、疼痛加剧或步态恶化的患者。



### **3. 游戏化康复（Physio-Quest）**

- **姿态追踪训练**：利用摄像头或传感器识别动作完成度，实时反馈。
- **任务与奖励**：完成每日任务获得经验值、徽章，解锁新关卡与搞笑剧情以激励用户继续训练。
- **共享就诊**：患者与治疗师可同步查看训练记录与进展。
- **设备日历**：集成可穿戴设备数据，展示每日活动环、睡眠等。



### **4. 数据生成与模拟（Data）**

- **合成患者数据集**：生成 40 名青少年患者的 30 天康复数据，包含步态、足底压力、心脏、睡眠、营养、症状、用药等。
- **中文 SOAP 病历**：为每位患者生成最近一次病历（主观、客观、评估、计划）。
- **动态动作指标**：为每个康复动作生成临床量化指标（如踝关节活动度、肌电、平衡时间等）。
- **时间表模拟**：生成患者每日时间线，包含能量与疼痛水平。
- **医生排班模拟**：生成 9 月 1–30 日医生每小时排班，每个会诊时段内嵌处方空位。

---



## **🏗️ 系统架构**

text

```
┌─────────────────────────────────────────────────────────────┐
│                        数据层 (Data)                         │
│  - 合成患者数据集 (JSON)                                      │
│  - 步态/足底压力/心脏/睡眠/营养/症状/用药                        │
│  - SOAP 病历与处方动作                                        │
│  - 医生排班与时间表模拟                                        │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                     患者端 (Patient)                         │
│  - 每日康复计划与游戏化训练                                     │
│  - 症状记录与设备数据同步                                       │
│  - 时间表视图                                                 │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                   治疗师端 (Therapist)                       │
│  - 患者仪表板与趋势报告                                        │
│  - 处方管理与会诊笔记                                          │
│  - 排班与预约                                                 │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                 游戏化康复 (Physio-Quest)                     │
│  - 姿态追踪训练                                               │
│  - 任务、奖励、共享就诊                                        │
│  - 设备日历                                                  │
└─────────────────────────────────────────────────────────────┘
```

---



## **📁 目录结构与文件说明**

> 以下为基于项目功能的推断结构，**实际请以仓库文件为准**。

text

```
ELAK-Physicalcare-therapy/
├── README.md                          # 项目说明文档
├── data/                              # 数据生成与模拟
│   ├── deepseek_python_*.py           # 合成患者数据集生成器（中文版）
│   ├── stepheal_youth_v10_zh.json     # 40 名青少年患者 30 天数据
│   ├── 青少年时间表.json               # 患者每日时间线模拟
│   └── doctor_schedule_september.json # 医生 9 月排班与处方空位
├── patient/                           # 患者端应用
│   ├── index.html                     # 患者主页
│   ├── clinic.js                      # 康复训练与数据记录逻辑
│   ├── style.css                      # 样式
│   └── assets/                        # 图片、图标等
├── therapist/                         # 治疗师端应用
│   ├── dashboard.html                 # 仪表板页面
│   ├── dashboard.js                   # 数据可视化与交互
│   ├── dashboard.css                  # 样式
│   └── assets/
├── physio-quest/                      # 游戏化康复模块
│   ├── index.html                     # 游戏主界面
│   ├── app.js                         # 姿态追踪与任务逻辑
│   ├── quest.css                      # 样式
│   ├── shared-visit/                  # 共享就诊功能
│   └── device-calendar/               # 设备日历
└── docs/                              # 文档与设计稿
    ├── architecture.md
    └── data-dictionary.md
```



### **各文件详细功能**


| **文件/目录**                             | **功能描述**                                                                                    |
| ------------------------------------- | ------------------------------------------------------------------------------------------- |
| `data/deepseek_python_*.py`           | 生成 40 名青少年患者的 30 天康复数据，包含步态、足底压力、心脏、睡眠、营养、症状、用药、康复动作指标等；生成中文 SOAP 病历；支持 Apple Watch 数据缺失处理。 |
| `data/stepheal_youth_v10_zh.json`     | 生成的合成数据集，每位患者包含 `patient_id`、`condition`、`daily_records`、`latest_medical_record` 等字段。       |
| `data/青少年时间表.json`                    | 模拟患者每日时间线，包含能量水平、疼痛水平、训练计划与实际完成情况、归因（如疲劳、社交冲突）。                                             |
| `data/doctor_schedule_september.json` | 医生 9 月排班，每小时一个 slot，预约时段内嵌 `prescription: null` 空位供填写处方，非预约时段标记 `prescription_slot: true`。  |
| `patient/index.html`                  | 患者端入口，展示每日康复计划、训练按钮、症状记录表单。                                                                 |
| `patient/clinic.js`                   | 处理训练完成逻辑、数据上传、与后端 API 交互、本地存储。                                                              |
| `therapist/dashboard.html`            | 治疗师仪表板，展示患者列表、趋势图表、处方管理。                                                                    |
| `therapist/dashboard.js`              | 数据可视化（Chart.js 或 D3）、筛选、排序、处方保存。                                                            |
| `physio-quest/index.html`             | 游戏化康复主界面，包含姿态追踪画布、任务列表、奖励展示。                                                                |
| `physio-quest/app.js`                 | 调用摄像头或传感器，识别动作，计算完成度，更新积分与徽章。                                                               |
| `physio-quest/shared-visit/`          | 患者与治疗师共享就诊记录，实时同步训练数据。                                                                      |
| `physio-quest/device-calendar/`       | 展示可穿戴设备数据（活动环、睡眠、心率），与训练任务关联。                                                               |


---



## **🧪 数据格式示例**



### **患者每日记录（**`daily_records` **片段）**

json

```
{
  "date": "2026-09-01",
  "device_info": { "has_apple_watch": true },
  "activity_rings": {
    "move_kcal": 450,
    "exercise_minutes": 35,
    "stand_hours": 10,
    "step_count": 7500
  },
  "cardiac": {
    "hrv_ms": 55.2,
    "resting_hr_bpm": 62,
    "walking_hr_bpm": 95
  },
  "gait": {
    "walking_asymmetry_pct": 5.2,
    "walking_speed_mps": 0.65,
    "cadence_steps_per_min": 88
  },
  "plantar_pressure": {
    "left_foot": { "hallux": 120.5, "midfoot": 50.2 },
    "right_foot": { "hallux": 110.3, "midfoot": 48.7 }
  },
  "rehab": {
    "exercise_completed": true,
    "exercise_accuracy_pct": 82.0,
    "pain_vas": 3.5
  }
}
```



### **医生排班片段（含处方空位）**

json

```
{
  "hour": "09:00-10:00",
  "type": "appointment",
  "patient_id": "Y017",
  "appointment_type": "复诊",
  "prescription": null,
  "prescription_slot": false,
  "notes": "复诊 - 患者 Y017"
}
```

---



## **🚀 快速开始**



### **环境要求**

- Python 3.8+
- Node.js 14+（如需运行前端）
- 现代浏览器（Chrome / Edge / Safari）



### **生成数据集**

bash

```
cd data
python deepseek_python_20261003_b763d9.py
# 生成 stepheal_youth_v10_zh.json
```



### **运行患者端**

bash

```
cd patient
# 使用任意静态服务器，例如：
python -m http.server 8000
# 浏览器打开 http://localhost:8000
```



### **运行治疗师端**

bash

```
cd therapist
python -m http.server 8001
# 浏览器打开 http://localhost:8001/dashboard.html
```



### **运行游戏化康复**

bash

```
cd physio-quest
python -m http.server 8002
# 浏览器打开 http://localhost:8002
```

---



## **🛠️ 技术栈**

- **数据生成**：Python, NumPy, JSON
- **前端**：HTML5, CSS3, JavaScript (ES6+)
- **可视化**：Chart.js / D3.js（推断）
- **姿态追踪**：MediaPipe / TensorFlow.js（推断）
- **数据存储**：JSON 文件 / 本地存储 / 可选后端 API
- **可穿戴设备**：Apple Watch 数据模拟

---



## **🤝 贡献指南**

欢迎提交 Issue 和 Pull Request。请确保：

1. 代码风格一致。
2. 新增功能附带测试数据或说明。
3. 更新 README 中对应的文件说明。

---



## **📬 联系方式**

- 仓库维护者：090817
- 项目链接：[https://github.com/090817/ELAK-Physicalcare-therapy](https://github.com/090817/ELAK-Physicalcare-therapy)

