---
title: 加入我们
description: 如何把你们的芯片、本体或软件接进 RV-EAI：四类参与方式、认领清单、兼容矩阵与参与阶梯。
lead: 这份方案的价值取决于接进来的人有多少。不管你在哪一层，只要能跑通一个可插拔点，就可以把结果放进兼容矩阵。
---

## 我们欢迎谁

<div class="grid-cards">
<div class="card">
<h3>芯片与模组厂商</h3>
<p>把你的 BSP、算子库与推理运行时接进一层：本体层给驱动与 FOC 方案，小脑层给实时核与总线，大脑层给 NPU / AI CPU 与 SDK。</p>
</div>
<div class="card">
<h3>本体与整机厂商</h3>
<p>提供关节、总线与传感器接口，和我们一起把「参考整机」从一台扩成一组。青龙 Mini / NanoLoong 之后还需要更多本体。</p>
</div>
<div class="card">
<h3>集成商与高校</h3>
<p>拿参考镜像做场景试点，或把课程套件建在这套栈上；高校也可以直接认领兼容性测试的一部分。</p>
</div>
<div class="card">
<h3>个人开发者</h3>
<p>跑通一个模型、补一个 ROS 包、修一个算子，都是有效贡献。仓库开源、结果进矩阵，不看单位看结果。</p>
</div>
</div>

## 五个可插拔点，任选其一认领

| 可插拔点 | 需要你提供的 | 我们会做的 |
| --- | --- | --- |
| ① 本体：电机与连接 | 驱动器 / MCU / 模组的 BSP 或数据手册、上板实测 | 接入参考整机，记录到兼容矩阵 |
| ② 小脑：实时控制 | 实时核型号与 TCM 规格、CAN-FD / EtherCAT 接口、RTOS 移植 | 双域镜像适配，做毫秒级闭环验证 |
| ③ 大脑：AI 算力 | NPU / AI CPU 规格、算子覆盖清单、推理 SDK | 跑本地 LLM / VLM / VLA，给出带条件的实测 |
| ④ 操作系统 | 发行版的 RISC-V 镜像、ROS 2 包供给情况 | 纳入五发行版矩阵，做真机回归 |
| ⑤ AI 框架与模型 | 运行时或模型权重、适配说明 | 纳入三条框架路线之一，记录可用性 |

> **判定很简单：** 换掉这一个点之后，其余四点不需要改动，上层也不需要重新适配——通过即为合格。

## 参与阶梯

<ul class="timeline">
<li><span class="t-when">Step 1</span><div class="t-what"><b>跑通</b> —— 在参考镜像上把你的部件跑起来，留下日志与复现命令。</div></li>
<li><span class="t-when">Step 2</span><div class="t-what"><b>提交结果</b> —— 把「型号 + 条件 + 结果」提交进仓库的兼容性记录（条件必须写全：构建版本、线程数、量化格式）。</div></li>
<li><span class="t-when">Step 3</span><div class="t-what"><b>进兼容矩阵</b> —— 由工作组复核，进入公开的兼容矩阵，成为推荐组合的一部分。</div></li>
<li class="plan"><span class="t-when">Step 4 <span class="tag-plan">规划</span></span><div class="t-what"><b>参考整机 / 场景试点</b> —— 愿意提供整机的伙伴，一起做工业或服务场景的参考实现。</div></li>
</ul>

## 我们会给你什么

- **接口清单**：三层硬件与四层软件的接口定义，以及五个可插拔点的边界。
- **参考镜像**：openKylin + ROS 2 + RT-Thread 双域镜像（K3 / A210 / Titan 可复现）。
- **评测方法**：怎么测、条件怎么记、结果怎么公示——避免「跑分对不上」的扯皮。
- **公开署名**：进入兼容矩阵的部件会写清型号与提供方，不埋名。

## 我们不会要求你什么

- 不需要独占授权，也不要求你放弃自己的商业版本；
- 不要求统一到某一个框架或某一颗芯片——三条框架路线并存就是这个意思；
- 不要求你现在就有整机，一个可插拔点跑通就算进来。

## 怎么联系

| 渠道 | 地址 |
| --- | --- |
| 邮件 | [wuwei@rv2036.org](mailto:wuwei@rv2036.org) |
| 社区 | [rv2036.org](https://rv2036.org) · 甲辰计划 · openKylin 社区 · FlagOS 社区 |
| 代码与 issue | [仓库地址](https://github.com/kubuds/RV-EAI) |
| 招募 | 甲辰计划 · openKylin 社区 · FlagOS 社区持续招募开源实习生与生态伙伴 |

<div class="cta-band" style="margin-top:2.2rem">
<div>
<h2>来一起做一些好玩的机器人吧</h2>
<p>带上你的芯片、本体或者一段能跑通的代码，我们把接口对上。</p>
</div>
<div><a class="btn" href="mailto:wuwei@rv2036.org">发邮件给我们 →</a></div>
</div>
