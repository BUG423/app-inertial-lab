# 📱 app-inertial-lab

[![Release](https://img.shields.io/github/v/release/BUG423/app-inertial-lab?color=brightgreen)](https://github.com/BUG423/app-inertial-lab/releases)
[![Android](https://img.shields.io/badge/Android-API%2026%2B-3DDC84.svg?logo=android&logoColor=white)](https://developer.android.com)
[![Kotlin](https://img.shields.io/badge/Kotlin-2.0-7F52FF.svg?logo=kotlin&logoColor=white)](https://kotlinlang.org)
[![LiteRT](https://img.shields.io/badge/LiteRT-TFLite-FF6F00.svg?logo=tensorflow&logoColor=white)](https://ai.google.dev/edge/litert)
[![ARCore](https://img.shields.io/badge/ARCore-VIO%20Track-4285F4.svg?logo=google&logoColor=white)](https://developers.google.com/ar)
[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC_BY--NC--ND_4.0-red.svg)](https://creativecommons.org/licenses/by-nc-nd/4.0/)

> **app-inertial-lab** 是面向惯性定位与端侧科学计算的高精度 Android 采集实验、真机轨迹对齐与端侧轻量化模型评测平台。融合高精 200Hz 原始 IMU 采集、Google ARCore VIO 局部参考轨迹对齐与 LiteRT 端侧前向推理。

---

## 📥 快速下载与安装

平台已发布正式构建版本，支持在 Android 8.0+ 真机上直接安装使用：

👉 **[点击前往 Releases 发布页面下载 APK 安装包 (v1.1.0)](https://github.com/BUG423/app-inertial-lab/releases/latest)**

---

## 🖼️ 核心功能与架构预览

| 传感器规范采集与无损交换链路 | 实验指标与技术规格 |
| :---: | :---: |
| 200Hz 原始 IMU (比力+角速度) $\to$ `.iplab` 归档 | Android 8.0+ / LiteRT / ARCore VIO |
| ARCore VIO 轨迹参考对齐 $\to$ 局部坐标解算 | ATE / RMSE / 端点漂移率 / p50-p99 延迟剖析 |

---

## 🎯 核心功能模块

- **📱 200Hz 规范硬件同步采集**：严格以陀螺仪硬件时钟为全局时间戳基准；具备硬件自适应协商，如实记录采样频率，杜绝端侧黑盒静默重采样。
- **🎨 ARCore VIO 实时参考对比**：结合 Google ARCore Sensor Pose，实时解算手机机体局部姿态与差分线速度，支持画布动态对比。
- **⚡ LiteRT 手机端侧批量推理**：支持基于 Google LiteRT 运行时加载 `.iplmodel` 自包含模型包，支持实时边采边测与多模型批量离线基准评测。
- **📊 科学指标全自动度量**：自动化输出绝对轨迹误差（ATE）、速度均方根误差（RMSE）、累积漂移率以及推理延迟分位数（p50 / p90 / p99）。
- **📦 标准化数据归档 (.iplab)**：自包含 ZIP 规范归档，内嵌 `manifest.json` 与 `data/sequence.csv`，并提供一键导出为 Canonical HDF5 的 Python 转换工具。

---

## ✨ 核心能力

- **⏱️ 零插值高保真**：硬件级时间对齐与缓冲落盘，保障科研数据真实可复现。
- **🧪 端侧全闭环**：无需依赖 PC 服务端，在移动终端即可完成“采集 - 对齐 - 推理 - 评测 - 出报告”。
- **🔒 隐私安全无侵扰**：相机图像仅在 ARCore 底层算法内部消费，应用层绝对不捕获、不渲染、不缓存任何相机图像画面。

---

## 🚀 快速上手与工程构建

### 1. 数据转换与测试
```bash
# 安装 Python 工具依赖
python3 -m pip install -r requirements-dev.txt

# 将 .iplab 手机记录转换为科学 HDF5 数据集
python tools/convert_dataset.py recording.iplab -o ./datasets/converted/
```

### 2. Android 源码构建
```bash
# 编译 Debug 测试包
./gradlew assembleDebug
```

---

## 📄 知识产权与开源协议

本项目遵循 **[Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)](https://creativecommons.org/licenses/by-nc-nd/4.0/)** 严格非商业开源许可：

- ❌ **严禁商用**：任何个人或组织不得将本项目源码、编译产物或衍生版本用于任何商业盈利目的。
- ❌ **禁止演绎与分发修改版**：未经授权不得散布基于本项目修改后的二次分发版本。
- 🔒 **权利保留**：作者保留对本平台代码与架构的所有版权与法律追责权利。
