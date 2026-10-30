---
title: Architecture
description: The three hardware layers and four software layers of RV-EAI — body, cerebellum and brain with their options and interfaces, plus the ISA foundation and dual-domain system design.
lead: This page opens up each hardware layer and software layer, with the current option list, key specifications and the provenance of every number.
---

{{< arch >}}

## How the three layers split

The split is not about which layer is “smarter” but about **time scale**: the three layers are three orders of magnitude apart, so each needs a different hardware and software shape.

| Layer | Time scale | What it does | Silicon available today |
| --- | --- | --- | --- |
| Body | microsecond current loop | joint drives, FOC control, hybrid force/position control, sensor I/O, wireless | Zhongke Benyuan RV-FOC · HPMicro HPM5100 / HPM6E8Y · GigaDevice GD32V · WCH CH32V / CH32M030 · Espressif ESP32-C |
| Cerebellum | millisecond control loop | gait generation, balance, joint bus (CAN-FD / EtherCAT), real-time scheduling | SpacemiT K3 / SoM260 · Zhihe A210 · UltraRISC UR-DP1000 / Milk-V Titan |
| Brain | ten-millisecond inference | perception, understanding, planning, multimodal interaction, local LLM and VLA inference | SpacemiT K3 · Axera AX650N · Rockchip RK1828 |

> **The criterion has not changed:** can this layer plug in, and does it run once plugged in — not how high it scores. Performance is optimised by each vendor inside its own layer.

## Body: motors and I/O

The joint is the core component here. A humanoid robot has more than 14 rotary joints; each joint is a motor, an encoder and a controller board, with a RISC-V DSP doing FOC, hybrid force/position control and vibration suppression.

| Vendor | Part | Key specification | Provenance |
| --- | --- | --- | --- |
| Zhongke Benyuan | Joint motor solution | RISC-V DSP architecture driver, FOC operators in hardware | vendor material |
| HPMicro | HPM5100 | RISC-V 400 MHz mixed-signal MCU, 4×16-bit ADC (2 MSPS), four motors per chip | vendor release (2026-10-12) |
| HPMicro | HPM6E8Y | Robot-joint MCU, 1 μs current loop | vendor material |
| GigaDevice | GD32V series | First 32-bit general-purpose RISC-V MCU (GD32VF103, 2019); GD30DR8306 motor-drive platform | vendor material |
| WCH | CH32V407 | Qingke RISC-V core, RVV vector extension, dual 480 Mbps USB | vendor material |
| WCH | CH32M030 | Motor-control MCU with dual N pre-driver | vendor material |
| Espressif | ESP32-C series | In-house RISC-V, Wi-Fi + BLE, billions shipped | vendor material |

## Cerebellum: real-time control

The key design is **physical separation of the two domains**: AI compute and real-time control run in parallel on the same chip, real-time cores under RTOS closing joint loops, AI cores under Linux doing planning, without preempting each other.

| Platform | Part | Key specification | Provenance |
| --- | --- | --- | --- |
| SpacemiT | K3 / SoM260 | 8× RISC-V 2.4 GHz, RVA23, IME; 2 real-time cores + 3 MB TCM; 10× CAN-FD, 4× GbE (EtherCAT / TSN); ROS 2 Humble / Jazzy | vendor docs |
| Zhihe Computing | A210 | 8× RV64GCV (4×C920 + 4×C908), NPU 12 TOPS@INT8; AGIROS + openEuler verified on hardware | vendor datasheet + community announcement |
| UltraRISC | UR-DP1000 | 8× 2.0 GHz RV64GCBH, RVA22 compliant, RVA23-compatible (except V); Mini-ITX, PCIe Gen4 x16, 64 GB DDR4 ECC, UEFI + ACPI | vendor docs |
| Milk-V | Titan | Evaluation platform from the same family; finished the humanoid half-marathon (21.0975 km) in 2026-04 | vendor docs + public reports |

## Brain: on-board AI compute

There are two ways to assemble this layer: one RISC-V AI CPU carrying both real-time and inference, or an AI co-processor next to the host SoC (over PCIe / USB) so compute and host upgrade independently.

| Platform | Part | Key specification | Provenance |
| --- | --- | --- | --- |
| SpacemiT | K3 | 60 TOPS (INT4 sparse peak); AI and real-time domains in parallel | vendor data (peak) |
| Axera | AX650N | Mixed-precision NPU 43.2 TOPS@INT4 / 10.8 TOPS@INT8; 8K ISP; under 8 W per board; CLIP / SAM / DINOv2 / Qwen2 / DeepSeek R1 adapted | vendor data |
| Rockchip | RK1828 | 3× 64-bit RISC-V cores (2 with 128-bit vector units); NPU 20 TOPS@INT8; 5 GB on-package DRAM at 1 TB/s; PCIe 2.1 / USB 3.0 | vendor data |

### Our measurements (footnote)

On a SpacemiT K3 board (Bianbu 4.0.7, kernel 6.18.3, collected 2026-10-21): 1B VLM 24.09 t/s and 24B MoE 12.00 t/s (both Q4_K_M, llama.cpp 0.1.9, AI cores, 8 threads); IME2 970 GMAC/s on one core and 5632 GMAC/s on eight threads (vendor kernel).

These numbers are **footnotes and Q&A material only**, not the claim of this solution: TOPS is a paper peak, while usable throughput depends on memory bandwidth, operator coverage and thread scheduling.

## Instruction set: use what is there

One ISA across all three layers, with extensions taken as needed:

| Extension | Purpose | Status |
| --- | --- | --- |
| RVV (vector) | general vector compute, convolution, codecs | working on K3 |
| IME (matrix) | matrix multiply-add for Transformers and LLM inference | working on K3 (single- and multi-thread verified) |
| AME | the other matrix-extension route | experimental support in FlagOS |
| VME | further vector/matrix extensions | tracks community and silicon |

> **An engineering conclusion:** on K3, RVV widening multiply-add reaches roughly 31.94 GMAC/s per core, while IME's vmadot reaches roughly 204 GMAC/s. That is why matrix extensions (IME / AME) are a requirement rather than a bonus — but we state it as an engineering judgement, not as a competitive claim.

## Operating system: five distributions plus one RTOS

| Domain | System | Responsibility |
| --- | --- | --- |
| Brain | openKylin / Debian / Ubuntu / Fedora / openEuler | AI and robotics software stack, ROS 2, containers and toolchains |
| Cerebellum | RT-Thread | real-time scheduling, joint bus (CAN-FD / EtherCAT), sensor I/O |

The two domains cooperate over **rpmsg / shared memory / PCIe**; the K3 real-time system and rpmsg examples are open source. One SDK covers both domains, so developers keep a familiar open-source ecosystem without lock-in.

## AI framework layer: three parallel routes

| Route | What it is | Status |
| --- | --- | --- |
| FlagOS | Open unified AI system software stack (led by BAAI): FlagGems / FlagScale / FlagCX / FlagPerf / FlagOS-Robo; RISC-V is on the official roadmap (RVV / IME / AME) | 18 chip vendors · 32 chips · 497 operators |
| llama.cpp | Community route, natively compiled for K3 (AI cores + IME2); runs YOLO detection, local VLM inference and text embedding | working |
| TileLang | Python-side compilation for high-performance operators; the CPU path is still scalar and improves with the community | verified |
| Vendor runtimes | Vendor-optimised inference engines and SDKs (e.g. SpaceMIT ORT EP), complementary to the two above | pluggable |

### Engineering measurement (footnote)

ncnn's original int8 path (vmacc) was 4–9× slower than fp32 on K3; dequantising int8 weights back to fp32 at load time and running the mature kernels made convolution-heavy backbones 2.9–9.2× faster (vgg16 9.2×, mobilenet 8.8×, resnet18 6.0×). Across 35 models, **8 clearly benefited, 20 stayed level and 7 were about 10% slower** — a per-model choice, not a blanket rule.

## Model layer: four categories, closed loop on device

| Category | Models | Status on K3 |
| --- | --- | --- |
| Perception | VAD · YOLO detection · SLAM · RGBD / lidar | deployed locally (rivision repository, open source) |
| Interaction | ASR (Whisper) · TTS · multimodal dialogue | deployed locally (llama.cpp VLM + embedding service) |
| Decision | Nav2 navigation (2D lidar + RGBD) · task planning | launch package open sourced, differential-drive robots supported |
| Embodied | VLA / WAM: RoboBrain 2.0 · Qwen-VL · π0.5 · GR00T N1.7 | layered combination under verification |

### VLA measurement (footnote)

On the same K3 board: smolVLA 0.5B takes 7.5 s per action (ONNX, two 512×512 cameras); ACT grasping takes 2.59 s (int8); a VLA above 2B takes over 45 minutes per inference (GO-1 measured 2705 s) and needs an NPU. The recommended combination is therefore layered: **RoboBrain for planning, smolVLA for execution**.
