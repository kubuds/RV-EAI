---
title: 来源与许可
description: 本站图片、字体、数据来源与许可证说明：所有图表为自绘，不加载网络字体，不引用第三方照片。
lead: 这一页把「图上每一个像素从哪来」讲清楚。我们刻意不引用任何第三方照片、产品图或 logo，避免授权风险。
---

## 图片：全部为自绘 SVG

站内所有图形都由本项目用 SVG 手写生成，没有位图、没有截图、没有厂商宣传图。当前清单：

| 图形 | 位置 | 说明 | 许可 |
| --- | --- | --- | --- |
| 人形机器人剖面（三层高亮） | 首页 | 自绘线条图，用于说明本体 / 小脑 / 大脑的分区 | Apache-2.0 |
| 三层时间尺度图（μs / ms / 10 ms） | 首页首屏 | 自绘，示意三层实时性差异 | Apache-2.0 |
| 架构总览图（三层硬件 + 四层软件） | 架构页 | 自绘，依据发布蓝图重绘为网页版 | Apache-2.0 |
| favicon 与品牌色块 | 全站 | 自绘几何图形 | Apache-2.0 |

> 原始蓝图中包含若干现场照片与厂商资料配图（例如关节电机方案示意图、装机实拍、真机跑步照）。这些素材的版权分属各厂商与社区，**本站一律不引用**，改以自绘示意图替代。

## 字体：只使用系统字体栈

页面不加载任何网络字体（无 Google Fonts、无自托管 woff），因此不涉及字体授权：

```
-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue",
"PingFang SC", "Hiragino Sans GB", "Microsoft YaHei",
"Source Han Sans SC", "Noto Sans CJK SC", sans-serif
ui-monospace, SFMono-Regular, Menlo, Consolas, "Liberation Mono", monospace
```

渲染结果取决于访问者操作系统的默认字体，不存在分发行为，也不产生字体许可费用。

## 品牌与商标

文中出现的 RISC-V、openKylin、OpenLoong、Milk-V、超睿科技、进迭时空、知合计算、爱芯元智、瑞芯微、先楫半导体、兆易创新、沁恒微电子、乐鑫科技、RT-Thread、FlagOS、llama.cpp、TileLang、ROS 2 等名称与型号，均为其各自所有者的商标或产品名，仅用于事实性指代与描述，**本站不使用其 logo 或视觉标识**。

## 数据来源与口径

页面上的每个数字都标注了口径，分四类：

| 口径标记 | 含义 | 举例 |
| --- | --- | --- |
| 厂商数据 / 厂商文档 | 来自芯片或软件厂商公开资料，未经本站独立复测 | K3 的 60 TOPS（INT4 稀疏峰值）、HPM6E8Y 的 1 μs 电流环 |
| 本团队实测 | 苦芽科技在 K3 真机（Bianbu 4.0.7 / 内核 6.18.3 / 2026-10-21）上跑出，条件随数字标注 | 1B VLM 24.09 t/s、24B MoE 12.00 t/s、IME2 970 / 5632 GMAC/s |
| 社区与生态材料 | 来自开源社区公开进展与公告 | openKylin ROS SIG 的 228/228 包入源、工作组成立（2026-06-25） |
| 规划 | 工作组内部规划，以社区决策为准，不构成承诺 | ROS SIG 2026-12 之后节点、工作组路线图五步 |

主要公开来源（按类别）：

- **RISC-V 产业**：riscv.org、NVIDIA 官方博客（2024 年 RISC-V 核心出货）、Meta MTIA 博客、Google Coral NPU 开发者博客、RISC-V Summit China 2025（Krste Asanovic 扩展路线图）
- **芯片与板卡**：进迭时空（spacemit.com）、知合计算（developer.zhcomputing.com）、Milk-V（milkv.io）、超睿科技、爱芯元智（axera-tech.com）、瑞芯微（rock-chips.com）、先楫半导体（hpmicro.com）、兆易创新（gigadevice.com）、沁恒微电子（wch.cn）、乐鑫科技（espressif.com）、中科本原
- **社区与生态**：openKylin 社区（含 ROS SIG 与具身智能工作组公告）、OpenLoong 项目页、AGIROS 社区、智源研究院 FlagOS、llama.cpp / TileLang / ncnn 上游仓库、ROS 2 文档
- **模型**：智源 RoboBrain 2.0、NVIDIA GR00T、Physical Intelligence π0.5、Qwen-VL 等公开模型页

> 完整来源清单（含条目编号、采集时间与待补数据说明）随发布材料维护在仓库 `whitepapers/` 与发布交付包的 `cite.txt` 中。

## 内容许可

- 站点文字与自绘图表：**Apache-2.0**（见仓库根目录 `LICENSE`）。
- 文中引用的第三方数据与名称：版权归原出处，本站仅作引用与事实性描述，引用时标注口径与来源类别。
- 若你是权利人并认为某处引用不当，请发邮件到 [wuwei@rv2036.org](mailto:wuwei@rv2036.org)，我们会立即处理。

## 后续若要放入第三方素材

我们的内部规则是「先登记、再上线」：

1. 必须记录 **原始 URL + 许可证（SPDX 标识）+ 抓取日期**，并在本页列出；
2. 优先使用 CC0 / CC-BY / 明确开源许可的素材，并按要求署名；
3. 厂商产品图、现场照片需要**书面授权**（邮件即可），否则一律改用自绘示意图；
4. 任何情况下不放入来源不明的图片、不使用厂商 logo 作为装饰、不嵌入网络字体。
