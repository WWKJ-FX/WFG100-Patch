# WFG100 Flight-Controller Patches

开源仓库 · 让 **物唯科技 WFG100** 飞控板卡即刻兼容 **ArduPilot Copter** 与 **Betaflight** 最新主线固件  
> 提供一键补丁、编译与刷写脚本，并附硬件手册与接线图 PDF

---

## 📦 仓库结构

| 路径 / 文件                                  | 说明 |
| ------------------------------------------- | ---- |
| `WFG100_APM_Copter-4.5x-4.6.x.patch`        | 针对 ArduPilot Copter 4.5/4.6 的增量补丁 |
| `WFG100_BF-4.5.X-4.6.X.patch`               | 针对 Betaflight 4.5/4.6 的增量补丁 |
| `Doc/`                                      | PDF 硬件手册 & 引脚、接线说明 |
| `README.md`                                 | 使用指南（本文） |



---

## ⚡ 快速开始

### 1. 环境准备  
| 工具 | 建议版本 |
| ---- | -------- |
| **Git** | ≥ 2.25 |
| **arm-none-eabi-gcc** | ≥ 10.3 |
| **Python** | ≥ 3.8 |
| **CMake / Ninja** | Betaflight 构建需要 |
| **waf** | ArduPilot 构建自带 |

### 2. 克隆代码
```bash
git clone https://github.com/WWKJ-FX/WFG100-Patch.git
```

### 3. 获取并切换到对应固件源码  
示例（ArduPilot Copter 4.6.0）：
```bash
git clone https://github.com/ArduPilot/ardupilot.git
cd ardupilot
git checkout Copter-4.6.0
```

### 4-A. 应用 **ArduPilot Copter** 补丁
```bash
git apply ../WFG100-Patch/WFG100_APM_Copter-4.5x-4.6.x.patch
./waf configure --board=WFG100
./waf copter -j$(nproc)         # 生成 build/WFG100/bin/arducopter.apj
```

### 4-B. 应用 **Betaflight** 补丁
```bash
git clone https://github.com/betaflight/betaflight.git
cd betaflight
git checkout BF-4.6.0
git apply ../WFG100-Patch/WFG100_BF-4.5.X-4.6.X.patch
make WFG100 -j$(nproc)          # 生成 obj/WFG100/WFG100.hex
```

### 5. 刷写固件  
- **ArduPilot**：`Mission Planner` / `QGroundControl` 选 `arducopter.apj`  
- **Betaflight**：`Betaflight Configurator` 选 `WFG100.hex`  
> 初次连接若无心跳，请检查 USB 驱动或重新刷写。

---

## 🧩 常见问题

| 现象 | 可能原因 & 处理 |
| ---- | --------------- |
| `error: patch failed` | 固件版本与补丁基线不符，确认 tag 或 commit |
| `WFG100` 未知板卡 | `./waf configure` 前补丁未生效，重跑 `git apply` |
| Mission Planner 无心跳 | 刷写不完整或 USB 驱动缺失，重刷 & 驱动重装 |
| CAN 外设不工作 | 确认 `CAN_P1_DRIVER=1`、终端电阻 120 Ω 完备 |

---

## 📚 文档

| 文件 | 内容 |
| ---- | ---- |
| `Doc/WFG100-硬件手册-APM-20250718.pdf` | 板卡硬件、引脚、电气指标，ArduPilot 接线示例 |
| `Doc/WFG100-硬件手册-BF-20250718.pdf`  | Betaflight 专用资源映射、PID 调参建议 |

> PDF 内容均可自由分发，引用时请保留物唯科技版权标识。

---

## 🤝 贡献指南

1. Fork → 新建分支 → 提交 PR  
2. PR 请附 **修改点说明**、测试日志与目标固件版本  
3. 对硬件问题可在 Issues 贴图、贴 log；我们会尽快响应  

---

## 📜 许可证

本仓库除 `Doc/*.pdf` 图片与商标外，其他内容均采用 **MIT License**。  
商业使用请遵守 MIT 条款并保留版权声明。

---

## 📞 联系与支持

- **Issue**：首选，统一跟踪  
- **邮箱**：xudarong@wwzhyun.cn
- **QQ 群**：179208785

---

> © 2025 Guangzhou Wuwei Tech. Happy flying! ✈️
