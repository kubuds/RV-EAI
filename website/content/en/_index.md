---
title: Overview
description: RV-EAI is an open RISC-V solution for embodied AI — one ISA across body, cerebellum and brain, five pluggable points, several vendors per layer, all demonstrated.
lead: This site turns the architecture blueprint released at the 2026 Wuzhen Internet Light event into engineering material you can actually use — how the three layers split, who is in each layer, where the interfaces are, and how to plug in.
---

{{< stage >}}

<div class="layer-step" id="layer-body" data-zone="body">
<span class="step-tag">Body · motors &amp; I/O · μs</span>

### The joint is the core of this layer

A humanoid robot has more than 14 rotary joints (shoulder, elbow, waist, hip); each joint is a motor, an encoder and a controller board. This layer is already **RISC-V all the way through**: joint drives, sensor I/O and wireless connectivity all have domestic RISC-V silicon to choose from.

<div class="vendor-grid">
  <div class="vendor">
    <div class="vname">Zhongke Benyuan</div>
    <div class="vpart">Joint motor solution</div>
    <p>RISC-V DSP-architecture driver that moves the FOC operators into hardware, aimed at joint motors.</p>
  </div>
  <div class="vendor">
    <div class="vname">HPMicro</div>
    <div class="vpart">HPM5100 / HPM6E8Y</div>
    <p>400 MHz mixed-signal MCU, 4×16-bit ADC (2 MSPS), four motors from one chip; HPM6E8Y targets robot joints.</p>
  </div>
  <div class="vendor">
    <div class="vname">GigaDevice</div>
    <div class="vpart">GD32V series</div>
    <p>Shipped the first 32-bit general-purpose RISC-V MCU in 2019 (GD32VF103); paired with the GD30DR8306 motor-drive platform.</p>
  </div>
  <div class="vendor">
    <div class="vname">WCH</div>
    <div class="vpart">CH32V407 / CH32M030</div>
    <p>In-house Qingke RISC-V core; CH32V407 adds RVV vector extensions and dual 480 Mbps USB, CH32M030 is a motor-control MCU.</p>
  </div>
  <div class="vendor">
    <div class="vname">Espressif</div>
    <div class="vpart">ESP32-C series</div>
    <p>Self-developed RISC-V core with Wi-Fi + BLE — the robot's wireless link and cloud connection.</p>
  </div>
</div>

<div class="metrics">
  <div class="metric"><b>1 μs</b><span>Current-loop period</span><small>HPM6E8Y · vendor data</small></div>
  <div class="metric"><b>4 motors</b><span>From one MCU</span><small>HPM5100 · vendor data</small></div>
  <div class="metric"><b>Billions</b><span>RISC-V Wi-Fi MCUs shipped</span><small>ESP32-C · vendor data</small></div>
</div>

<p class="note"><b>Provenance:</b> figures marked “vendor data” come from public vendor material and were not independently re-measured by our team. Check the vendor's latest datasheet for exact part numbers and specifications.</p>
</div>

<div class="layer-step" id="layer-cerebellum" data-zone="cerebellum">
<span class="step-tag">Cerebellum · real-time control · ms</span>

### The real-time and AI domains are physically separated

Motion control needs a millisecond loop while inference works at tens of milliseconds. The key design here is that **the real-time cores and the AI cores live on the same die without stealing from each other** — the real-time cores run RTOS and close the joint loops, the AI cores run Linux and handle perception and planning, and the two domains meet over rpmsg, shared memory and buses.

<div class="vendor-grid">
  <div class="vendor">
    <div class="vname">SpacemiT</div>
    <div class="vpart">K3 / SoM260</div>
    <p>8× RISC-V 2.4 GHz, RVA23, IME; 2 dedicated real-time cores + 3 MB TCM; 10× CAN-FD and 4× GbE (EtherCAT / TSN).</p>
  </div>
  <div class="vendor">
    <div class="vname">Zhihe Computing</div>
    <div class="vpart">A210</div>
    <p>8× RV64GCV (4×C920 + 4×C908), NPU 12 TOPS@INT8; full AGIROS + openEuler stack verified on hardware (visual robotic-arm grasping).</p>
  </div>
  <div class="vendor">
    <div class="vname">UltraRISC / Milk-V</div>
    <div class="vpart">UR-DP1000 / Titan</div>
    <p>8× 2.0 GHz RV64GCBH, RVA22 compliant and RVA23-compatible (except V); Mini-ITX, PCIe Gen4 x16, 64 GB DDR4 ECC, UEFI + ACPI.</p>
  </div>
</div>

<div class="metrics">
  <div class="metric"><b>2 cores</b><span>dedicated real-time + 3 MB TCM</span><small>K3 · vendor data</small></div>
  <div class="metric"><b>10 lanes</b><span>CAN-FD + 4× GbE</span><small>K3 · vendor data</small></div>
  <div class="metric"><b>21.0975 km</b><span>humanoid half-marathon finished</span><small>Titan platform · 2026-04</small></div>
</div>

<p class="note"><b>How to choose:</b> deterministic work with a sub-millisecond period belongs on RTOS + MCU; trajectory planning and multimodal work belongs on Linux + AI cores. It is not either/or — it is a division of labour.</p>
</div>

<div class="layer-step" id="layer-brain" data-zone="brain">
<span class="step-tag">Brain · perception &amp; planning · 10 ms</span>

### Inference stays local, data stays on the robot

Vision and environment data from homes and factories should not go to the cloud. This layer is assembled by compute tier: one RISC-V AI CPU can carry both real-time and inference, or an AI co-processor can sit next to the host SoC over PCIe / USB so compute upgrades independently.

<div class="vendor-grid">
  <div class="vendor">
    <div class="vname">SpacemiT</div>
    <div class="vpart">K3</div>
    <p>60 TOPS (INT4 sparse peak, vendor data); AI and real-time domains run in parallel; local VAD / ASR / TTS / SLAM / VLA deployments verified.</p>
  </div>
  <div class="vendor">
    <div class="vname">Axera</div>
    <div class="vpart">AX650N</div>
    <p>Mixed-precision NPU 43.2 TOPS@INT4 / 10.8 TOPS@INT8; 8K ISP; board power under 8 W; CLIP / SAM / DINOv2 / Qwen2 / DeepSeek R1 adapted.</p>
  </div>
  <div class="vendor">
    <div class="vname">Rockchip</div>
    <div class="vpart">RK1828</div>
    <p>3× 64-bit RISC-V cores (two with 128-bit vector units); NPU 20 TOPS@INT8; 5 GB on-package DRAM at 1 TB/s; PCIe 2.1 / USB 3.0 to the host.</p>
  </div>
</div>

<div class="metrics">
  <div class="metric"><b>24.09 t/s</b><span>1B VLM, local</span><small>Q4_K_M · 8 threads on AI cores · our measurement</small></div>
  <div class="metric"><b>12.00 t/s</b><span>24B MoE, local</span><small>Q4_K_M · 8 threads on AI cores · our measurement</small></div>
  <div class="metric"><b>970 / 5632</b><span>GMAC/s (1 core / 8 threads)</span><small>IME2 · our measurement</small></div>
</div>

<p class="note"><b>Provenance:</b> “our measurement” figures were taken on a SpacemiT K3 board (Bianbu 4.0.7, kernel 6.18.3, collected 2026-10-21) with conditions stated next to every number. Vendor TOPS figures are peaks, not achievable throughput. Performance numbers are footnotes here, not the pitch.</p>
</div>

{{< /stage >}}

<section class="band alt">
<div class="wrap">
<div class="section-head">
<div class="kicker">Software stack</div>

## One ISA, two system domains, three framework routes

The brain domain runs a Linux distribution, the cerebellum domain runs RT-Thread, and the two cooperate over rpmsg, shared memory and buses. All three framework routes already work; none of them is mandatory.</div>

<div class="stack">
<div class="stack-row isa">
<div class="role">ISA foundation</div>
<div class="items"><span class="pill">RISC-V (RVA23)</span><span class="pill">RVV</span><span class="pill">IME</span><span class="pill">AME</span><span class="pill">VME</span></div>
</div>
<div class="stack-row">
<div class="role">Operating system</div>
<div class="items"><span class="pill">openKylin</span><span class="pill">Debian</span><span class="pill">Ubuntu</span><span class="pill">Fedora</span><span class="pill">openEuler</span></div>
</div>
<div class="stack-row">
<div class="role">RTOS</div>
<div class="items"><span class="pill">RT-Thread</span><span class="pill">rpmsg dual-domain</span><span class="pill">CAN-FD / EtherCAT</span></div>
</div>
<div class="stack-row">
<div class="role">AI frameworks</div>
<div class="items"><span class="pill">FlagOS</span><span class="pill">llama.cpp</span><span class="pill">TileLang</span><span class="pill">vendor runtimes</span></div>
</div>
<div class="stack-row">
<div class="role">Models</div>
<div class="items"><span class="pill">VAD / YOLO</span><span class="pill">SLAM</span><span class="pill">ASR / TTS</span><span class="pill">Nav2 / Planning</span><span class="pill">VLA / WAM</span></div>
</div>
</div>

<p class="note"><b>Dual domain:</b> one SDK covers both domains; developers keep the open-source ecosystem they already know, with no lock-in to a single commercial system. The K3 real-time system and rpmsg examples are open source.</p>
</div>
</section>

<section class="band">
<div class="wrap">
<div class="section-head">
<div class="kicker">Pluggable points</div>

## Five pluggable points — swap one, the other four stay

This is our testable definition of openness: replace any single point with another vendor's solution and the other four need no change, nor does the layer above.</div>

<div class="plugs">
<div class="plug">
<div class="n">01</div>
<h4>Body: motors &amp; I/O</h4>
<p>Joint drives, MCUs, wireless modules. Swapping the controller only means swapping the BSP.</p>
<span class="swap">Options: Zhongke Benyuan / HPMicro / GigaDevice / WCH / Espressif</span>
</div>
<div class="plug">
<div class="n">02</div>
<h4>Cerebellum: real-time control</h4>
<p>Real-time cores plus the RTOS control stack; the interface is the joint bus (CAN-FD / EtherCAT).</p>
<span class="swap">Options: K3 / A210 / UR-DP1000·Titan</span>
</div>
<div class="plug">
<div class="n">03</div>
<h4>Brain: AI compute</h4>
<p>NPU, AI CPU or co-processor, swapped by compute tier; the inference code above does not change.</p>
<span class="swap">Options: K3 / AX650N / RK1828</span>
</div>
<div class="plug">
<div class="n">04</div>
<h4>Operating system</h4>
<p>Linux distribution for the brain domain and an RTOS for the real-time domain, on one packaging standard.</p>
<span class="swap">Options: openKylin / Debian / Ubuntu / Fedora / openEuler</span>
</div>
<div class="plug">
<div class="n">05</div>
<h4>AI framework &amp; models</h4>
<p>Pick FlagOS, llama.cpp, TileLang or a vendor runtime; models follow the framework.</p>
<span class="swap">Options: three community routes + vendor SDKs</span>
</div>
</div>

<p class="note"><b>How it gets verified:</b> after swapping one point, the other four need no change and the layer above needs no re-adaptation, and the combination passes a conformance test. That is exactly what we are turning into specifications and a test suite next.</p>
</div>
</section>

<section class="band alt">
<div class="wrap">
<div class="section-head">
<div class="kicker">Joint release</div>

## Six organisations, three commitments

The release name “Qiyuan” is a working codename. What we publish is interfaces and inventories, not a frozen product.</div>

<div class="teams" style="margin-bottom:1.4rem">
<span class="team">openKylin community</span>
<span class="team">Milk-V</span>
<span class="team">UltraRISC</span>
<span class="team">Shanghai OpenLoong</span>
<span class="team">SpacemiT</span>
<span class="team">Kubuds Technology</span>
</div>

<div class="grid-cards">
<div class="card">
<h3>Fully open stack</h3>
<p>Chip BSPs, system enablement, the AI software stack and robot sample code are all released openly.</p>
</div>
<div class="card">
<h3>Reference hardware</h3>
<p>Reference boards and images based on K3 / A210 / Titan that you can reproduce and verify.</p>
</div>
<div class="card">
<h3>Open co-building</h3>
<p>More silicon, robot makers and integrators are welcome to help complete the compatibility matrix.</p>
</div>
</div>
</div>
</section>

<section class="band">
<div class="wrap">
<div class="cta-band">
<div>
<h2>Plug in at whichever layer suits you</h2>
<p>Demonstrate one of the five pluggable points and the result belongs in the compatibility matrix; if you can offer a robot platform, let's write the reference implementation together.</p>
</div>
<div>
<a class="btn" href="join/">Join us →</a>
</div>
</div>
</div>
</section>
