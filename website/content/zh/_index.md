---
title: 总览
description: RV-EAI 是基于 RISC-V 的具身智能开放解决方案：一套 ISA 贯穿本体、小脑与大脑，五个可插拔点，每一层都有多家可选、都已跑通。
lead: 这份站点把 2026 年乌镇互联网之光发布的架构蓝图整理成可查阅的工程材料：三层怎么分、每层有谁、接口在哪、怎么接进来。
---

{{< stage >}}

<div class="layer-step" id="layer-body" data-zone="body">
<span class="step-tag">本体 · 电机与连接 · μs</span>

### 关节是本体层的核心

一台人形机器人全身 14 个以上旋转关节（肩、肘、腰、髋），每个关节 = 电机 + 编码器 + 控制板卡。这一层已经做到**整链 RISC-V 化**：从关节电机驱动、传感接入到无线互联，都有国产 RISC-V 芯片可选。

<div class="vendor-grid">
  <div class="vendor">
    <div class="vname">中科本原</div>
    <div class="vpart">关节电机方案</div>
    <p>RISC-V DSP 架构驱动器，把 FOC 算子做进硬件，面向关节电机的高性能控制。</p>
  </div>
  <div class="vendor">
    <div class="vname">先楫半导体</div>
    <div class="vpart">HPM5100 / HPM6E8Y</div>
    <p>400 MHz 混合信号 MCU，4×16 位 ADC（2 MSPS），单芯片「一拖四」；HPM6E8Y 面向机器人关节。</p>
  </div>
  <div class="vendor">
    <div class="vname">兆易创新</div>
    <div class="vpart">GD32V 系列</div>
    <p>2019 年推出首颗 RISC-V 内核 32 位通用 MCU（GD32VF103）；配套 GD30DR8306 电机驱动平台。</p>
  </div>
  <div class="vendor">
    <div class="vname">沁恒微电子</div>
    <div class="vpart">CH32V407 / CH32M030</div>
    <p>自研青稞 RISC-V 内核；CH32V407 支持 RVV 向量扩展与双 480 Mbps USB，CH32M030 为电机控制 MCU。</p>
  </div>
  <div class="vendor">
    <div class="vname">乐鑫科技</div>
    <div class="vpart">ESP32-C 系列</div>
    <p>自研 RISC-V 内核的 Wi-Fi + BLE MCU，承担整机的无线互联与云端接入。</p>
  </div>
</div>

<div class="metrics">
  <div class="metric"><b>1 μs</b><span>电流环周期</span><small>HPM6E8Y · 厂商数据</small></div>
  <div class="metric"><b>一拖四</b><span>单芯片多电机</span><small>HPM5100 · 厂商数据</small></div>
  <div class="metric"><b>十亿颗级</b><span>RISC-V Wi-Fi MCU 出货</span><small>ESP32-C · 厂商数据</small></div>
</div>

<p class="note"><b>口径：</b>本层标注「厂商数据」的指标来自各厂商公开资料，未经本团队独立复测；具体型号与规格以厂商官网最新资料为准。</p>
</div>

<div class="layer-step" id="layer-cerebellum" data-zone="cerebellum">
<span class="step-tag">小脑 · 实时控制 · ms</span>

### 实时控制域与 AI 计算域物理隔离

运动控制要求毫秒级闭环，而推理是十毫秒级的事。这一层的关键设计是：**实时核与 AI 核在同一颗芯片上互不抢占**——实时核跑 RTOS 负责关节闭环，AI 核跑 Linux 负责感知与规划，两域通过 rpmsg / 共享内存 / 总线协同。

<div class="vendor-grid">
  <div class="vendor">
    <div class="vname">进迭时空</div>
    <div class="vpart">K3 / SoM260</div>
    <p>8 核 RISC-V 2.4 GHz，符合 RVA23，支持 IME；2 个独立实时核 + 3 MB TCM 紧耦合内存；10 路 CAN-FD + 4 路千兆以太网（EtherCAT / TSN）。</p>
  </div>
  <div class="vendor">
    <div class="vname">知合计算</div>
    <div class="vpart">A210</div>
    <p>8 核 RV64GCV（4×C920 + 4×C908），NPU 12 TOPS@INT8；已完成 AGIROS + openEuler 全栈实机验证（机械臂视觉抓取）。</p>
  </div>
  <div class="vendor">
    <div class="vname">超睿科技 / Milk-V</div>
    <div class="vpart">UR-DP1000 / Titan</div>
    <p>8 核 2.0 GHz RV64GCBH，RVA22 合规、兼容 RVA23（除 V）；Mini-ITX 主板，PCIe Gen4 x16、64 GB DDR4 ECC、UEFI+ACPI。</p>
  </div>
</div>

<div class="metrics">
  <div class="metric"><b>2 实时核</b><span>+ 3 MB TCM</span><small>K3 · 厂商数据</small></div>
  <div class="metric"><b>10 路</b><span>CAN-FD + 4 路千兆网</span><small>K3 · 厂商数据</small></div>
  <div class="metric"><b>21.0975 km</b><span>人形机器人半马完赛</span><small>Titan 平台 · 2026-04</small></div>
</div>

<p class="note"><b>选型建议：</b>控制周期小于 1 毫秒、任务确定的部分放 RTOS + MCU；需要轨迹规划与多模态的分支交给 Linux + AI 核。两颗不是二选一，而是分工。</p>
</div>

<div class="layer-step" id="layer-brain" data-zone="brain">
<span class="step-tag">大脑 · 感知理解规划 · 10 ms</span>

### 本地推理，数据不出本体

家庭与工业场景的视觉与环境数据不适合上云。这一层按算力档位组合：一颗 RISC-V AI CPU 可以同时承担实时与推理；也可以在主控 Soc 之外叠加 AI 协处理器，做到算力与主控解耦升级。

<div class="vendor-grid">
  <div class="vendor">
    <div class="vname">进迭时空</div>
    <div class="vpart">K3</div>
    <p>60 TOPS（INT4 稀疏峰值，厂商数据）；AI 计算域与实时控制域并行；VAD / ASR / TTS / SLAM / VLA 本地部署已做验证。</p>
  </div>
  <div class="vendor">
    <div class="vname">爱芯元智</div>
    <div class="vpart">AX650N</div>
    <p>混合精度 NPU 43.2 TOPS@INT4 / 10.8 TOPS@INT8；8K ISP；整板功耗 &lt; 8 W；已适配 CLIP / SAM / DINOv2 / Qwen2 / DeepSeek R1。</p>
  </div>
  <div class="vendor">
    <div class="vname">瑞芯微</div>
    <div class="vpart">RK1828</div>
    <p>3×64 位 RISC-V 核（2 核带 128 位向量单元）；NPU 20 TOPS@INT8；5 GB 片上 DRAM、1 TB/s 带宽；PCIe 2.1 / USB 3.0 接主控。</p>
  </div>
</div>

<div class="metrics">
  <div class="metric"><b>24.09 t/s</b><span>1B VLM 本地推理</span><small>Q4_K_M · AI 核 8 线程 · 本团队实测</small></div>
  <div class="metric"><b>12.00 t/s</b><span>24B MoE 本地推理</span><small>Q4_K_M · AI 核 8 线程 · 本团队实测</small></div>
  <div class="metric"><b>970 / 5632</b><span>GMAC/s（单核 / 8 线程）</span><small>IME2 · 本团队实测</small></div>
</div>

<p class="note"><b>口径：</b>「本团队实测」在进迭时空 K3 真机（Bianbu 4.0.7，内核 6.18.3，2026-10-21 采集）完成，条件随数字标注。厂商标称 TOPS 为峰值，不等于可用吞吐；性能数字只作脚注，不作为本方案的主张。</p>
</div>

{{< /stage >}}

<section class="band alt">
<div class="wrap">
<div class="section-head">
<div class="kicker">软件栈</div>

## 一个 ISA，两个系统域，三条框架路线

大脑域跑 Linux 发行版，小脑域跑 RT-Thread，两域通过 rpmsg / 共享内存 / 总线协同。框架层三条路线都已跑通，我们不做强制统一。</div>

<div class="stack">
<div class="stack-row isa">
<div class="role">指令集底座</div>
<div class="items"><span class="pill">RISC-V（RVA23）</span><span class="pill">RVV</span><span class="pill">IME</span><span class="pill">AME</span><span class="pill">VME</span></div>
</div>
<div class="stack-row">
<div class="role">操作系统层</div>
<div class="items"><span class="pill">openKylin</span><span class="pill">Debian</span><span class="pill">Ubuntu</span><span class="pill">Fedora</span><span class="pill">openEuler</span></div>
</div>
<div class="stack-row">
<div class="role">RTOS 层</div>
<div class="items"><span class="pill">RT-Thread</span><span class="pill">rpmsg 双域协同</span><span class="pill">CAN-FD / EtherCAT</span></div>
</div>
<div class="stack-row">
<div class="role">AI 框架层</div>
<div class="items"><span class="pill">FlagOS</span><span class="pill">llama.cpp</span><span class="pill">TileLang</span><span class="pill">厂商定制运行时</span></div>
</div>
<div class="stack-row">
<div class="role">模型层</div>
<div class="items"><span class="pill">VAD / YOLO</span><span class="pill">SLAM</span><span class="pill">ASR / TTS</span><span class="pill">Nav2 / Planning</span><span class="pill">VLA / WAM</span></div>
</div>
</div>

<p class="note"><b>双域协同：</b>一套 SDK 覆盖两个域；开发商沿用熟悉的开源生态，不绑定单一商业系统。K3 的实时系统与 rpmsg 示例已开源。</p>
</div>
</section>

<section class="band">
<div class="wrap">
<div class="section-head">
<div class="kicker">可插拔点</div>

## 五个可插拔点，替换一个其余四个不动

这是我们对「开放」的可验证定义：任意一个点换成另一家方案，其余四点不需要改动，也不需要重新适配上层。</div>

<div class="plugs">
<div class="plug">
<div class="n">01</div>
<h4>本体：电机与连接</h4>
<p>关节电机驱动器、MCU、无线模组。换主控只需换 BSP。</p>
<span class="swap">可换：中科本原 / 先楫 / 兆易 / 沁恒 / 乐鑫</span>
</div>
<div class="plug">
<div class="n">02</div>
<h4>小脑：实时控制</h4>
<p>实时核与 RTOS 侧控制栈，接口面向 CAN-FD / EtherCAT 关节总线。</p>
<span class="swap">可换：K3 / A210 / UR-DP1000·Titan</span>
</div>
<div class="plug">
<div class="n">03</div>
<h4>大脑：AI 算力</h4>
<p>NPU / AI CPU / 协处理器，按算力档位替换，上层推理代码不变。</p>
<span class="swap">可换：K3 / AX650N / RK1828</span>
</div>
<div class="plug">
<div class="n">04</div>
<h4>操作系统</h4>
<p>Linux 发行版与实时域 RTOS，同一套内核接口与打包规范。</p>
<span class="swap">可换：openKylin / Debian / Ubuntu / Fedora / openEuler</span>
</div>
<div class="plug">
<div class="n">05</div>
<h4>AI 框架与模型</h4>
<p>FlagOS / llama.cpp / TileLang / 厂商运行时四选一，模型侧跟随框架切换。</p>
<span class="swap">可换：三条社区路线 + 厂商 SDK</span>
</div>
</div>

<p class="note"><b>怎么验证：</b>换掉一个点之后，其余四点不需要改动、也不需要重新适配上层，并且能通过一致性测试——这就是我们下一步要写成规范与测试套件的东西。</p>
</div>
</section>

<section class="band alt">
<div class="wrap">
<div class="section-head">
<div class="kicker">联合发布</div>

## 六家单位联合发布，三项承诺

发布名称「启元」为工作代号。我们发布的是接口与清单，不是一台定型的整机。</div>

<div class="teams" style="margin-bottom:1.4rem">
<span class="team">openKylin 社区</span>
<span class="team">Milk-V</span>
<span class="team">超睿科技</span>
<span class="team">上海 OpenLoong</span>
<span class="team">进迭时空</span>
<span class="team">苦芽科技</span>
</div>

<div class="grid-cards">
<div class="card">
<h3>全栈开源</h3>
<p>芯片 BSP、系统适配、AI 软件栈、机器人示例代码全部开源发布。</p>
</div>
<div class="card">
<h3>参考整机</h3>
<p>提供基于 K3 / A210 / Titan 的参考整机与镜像，可复现、可验证。</p>
</div>
<div class="card">
<h3>开放共建</h3>
<p>欢迎更多芯片、本体与集成商加入，共同完善兼容矩阵。</p>
</div>
</div>
</div>
</section>

<section class="band">
<div class="wrap">
<div class="cta-band">
<div>
<h2>不管从哪一层接进来，都可以</h2>
<p>能跑通五个可插拔点中的一个，就把结果提交进兼容矩阵；愿意提供本体或整机的，我们一起来写参考实现。</p>
</div>
<div>
<a class="btn" href="join/">加入共建 →</a>
</div>
</div>
</div>
</section>
