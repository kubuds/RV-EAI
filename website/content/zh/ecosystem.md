---
title: 生态与路线图
description: openKylin 具身智能工作组与 OpenLoong 的协作进展，以及 ROS SIG 与工作组两条路线图。
lead: 软件与本体已经跑在一起。这一页记录协作是怎么发生的、现在到哪一步，以及接下来要做什么（规划部分以社区决策为准）。
---

## 组织：openKylin 具身智能工作组

2026-06-25 于开放原子开源生态大会正式成立，把原来的项目级协作升级为长期机制：**把「可接入」写成规范、测试与参考整机**。

成员单位包括上海苦芽科技、超睿科技、OpenLoong、海河实验室、麒麟软件、国防科技大学、中国长城等，覆盖芯片、操作系统、本体与高校四类角色。

## 里程碑：从联合适配到真机落地

<ul class="timeline">
<li><span class="t-when">2026-01-21</span><div class="t-what"><b>联合适配计划启动</b> —— openKylin + RISC-V + ROS 共同技术底座。</div></li>
<li><span class="t-when">2026-05-15</span><div class="t-what"><b>真机适配成功</b> —— 系统稳定运行，完成运动控制与基础交互演示。</div></li>
<li><span class="t-when">2026-06-25</span><div class="t-what"><b>具身智能工作组正式成立</b> —— 开放原子开源生态大会，四类角色同席。</div></li>
<li><span class="t-when">2026-07</span><div class="t-what"><b>加入 AGIROS 生态</b> —— ROS SIG 持续供给软件包。</div></li>
<li><span class="t-when">2026-10-18</span><div class="t-what"><b>RISC-V 中国峰会</b> —— 展示运行 openKylin 的 RISC-V 小型双足机器人。</div></li>
</ul>

## 本体：OpenLoong

OpenLoong 由开放原子开源基金会孵化、人形机器人（上海）有限公司运营，提供从全尺寸到教具型的完整开源硬件平台：

| 平台 | 定位 |
| --- | --- |
| 青龙 / 灵龙 | 全尺寸人形：43 自由度、182 cm、75 kg |
| 青龙 Mini | 强化学习小型平台 |
| NanoLoong | 开源双足教具，面向教学与课程套件 |

## 路线图一：openKylin ROS SIG

从「软件包供给」走向「机器人参考系统」。前五个节点为已发生事实，最后两个节点为规划。

<ul class="timeline">
<li><span class="t-when">2024-07</span><div class="t-what"><b>ROS SIG 成立</b></div></li>
<li><span class="t-when">2025-11</span><div class="t-what"><b>多架构验证完成</b>；2026-01 机器人计划启动。</div></li>
<li><span class="t-when">2026-02</span><div class="t-what"><b>100+ ROS 软件包完成打包</b></div></li>
<li><span class="t-when">2026-08</span><div class="t-what"><b>Jazzy ros-base 228 包通过三道本地验证</b>（bootstrap 构建 / 带测试重建 / 全新环境安装冒烟），推送 OKBS 四架构构建。</div></li>
<li><span class="t-when">2026-10</span><div class="t-what"><b>ros-base 228/228 四架构（含 riscv64）入 2.0 proposed 源，apt 可直接安装</b>；jazzy desktop 59 包就绪；3.0 Lyrical ros-base 230 包通过验证、CI 全绿。</div></li>
<li class="plan"><span class="t-when">2026-12 <span class="tag-plan">规划</span></span><div class="t-what">ros-base 随 2.0 版本节奏转正式源；desktop 增量入仓（解 CI 与系统包依赖）；3.0 ros-base 四架构构建完成。</div></li>
<li class="plan"><span class="t-when">2027 <span class="tag-plan">规划</span></span><div class="t-what">Nav2 / MoveIt 入仓；RISC-V 机器人参考镜像；多平台真机回归；openKylin 机器人版发布。</div></li>
</ul>

## 路线图二：具身智能工作组

把「处处可接入」写成规范、测试与参考整机。五个步骤全部为规划，**欢迎伙伴认领**。

<ul class="timeline">
<li class="plan"><span class="t-when">2026-Q4 <span class="tag-plan">规划</span></span><div class="t-what"><b>开放方案 v0</b> —— 三层接口清单 + 兼容矩阵初版 + K3 / Titan 参考软件栈。</div></li>
<li class="plan"><span class="t-when">2026-12 <span class="tag-plan">规划</span></span><div class="t-what"><b>参考镜像 v1</b> —— openKylin + ROS 2 + RT-Thread 双域镜像，K3 / A210 / Titan 可复现。</div></li>
<li class="plan"><span class="t-when">2027-Q1 <span class="tag-plan">规划</span></span><div class="t-what"><b>兼容性测试套件</b> —— 五个可插拔点的接口规范与一致性测试，CI 真机回归。</div></li>
<li class="plan"><span class="t-when">2027-Q2 <span class="tag-plan">规划</span></span><div class="t-what"><b>第二本体接入</b> —— 青龙 Mini / NanoLoong 教具平台 + 高校课程套件。</div></li>
<li class="plan"><span class="t-when">2027-H2 <span class="tag-plan">规划</span></span><div class="t-what"><b>场景试点与标准化</b> —— 工业 / 服务参考整机；接口规范进入社区标准；兼容矩阵 v2。</div></li>
</ul>

> **口径说明：** 上面标「规划」的节点均为工作组内部规划，以社区决策为准，不构成对外承诺。已发生的事实节点来源见「[来源与许可]({{< relref "licensing.md" >}})」页。

## 生态协同怎么落到工程上

- **软件侧**：openKylin 提供 RISC-V 版系统与 ROS 包供给，ROS SIG 负责软件包与质量门禁，具身智能工作组负责三层接口与兼容矩阵。
- **本体侧**：OpenLoong 提供整机与开源硬件平台，让「接口清单」有真实的关节、总线与传感器可以对接。
- **算力侧**：进迭时空、超睿、Milk-V 等提供参考平台，让每一层都有可复现的硬件底座。
- **验证侧**：苦芽科技负责把各层拼起来做端到端实测，并把结论写成本页与架构页里的口径。

<div class="cta-band" style="margin-top:2.2rem">
<div>
<h2>你的项目也可以是这条线上的一站</h2>
<p>不管是补一个软件包、接一块新本体，还是把兼容性测试跑在自家硬件上，都算进来。</p>
</div>
<div><a class="btn" href="{{< relref "join.md" >}}">加入共建 →</a></div>
</div>
