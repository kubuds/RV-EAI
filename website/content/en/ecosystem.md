---
title: Ecosystem & roadmap
description: Progress of the openKylin Embodied Intelligence Working Group and OpenLoong, plus the ROS SIG and working-group roadmaps.
lead: Software and hardware already run together. This page records how the collaboration happened, where it stands, and what comes next (planned items follow community decisions).
---

## Organisation: the openKylin Embodied Intelligence Working Group

Formed on 2026-06-25 at the OpenAtom open-source ecosystem conference, it upgrades project-level collaboration into a long-term mechanism: **writing “pluggable” down as specifications, tests and reference hardware**.

Members include Shanghai Kubuds Technology, UltraRISC, OpenLoong, Haihe Laboratory, KylinSoft, the National University of Defense Technology and China Greatwall — covering silicon, operating systems, robot platforms and universities.

## Milestones: from joint enablement to real hardware

<ul class="timeline">
<li><span class="t-when">2026-01-21</span><div class="t-what"><b>Joint enablement plan launched</b> — openKylin + RISC-V + ROS as a shared technical foundation.</div></li>
<li><span class="t-when">2026-05-15</span><div class="t-what"><b>Real hardware adaptation succeeded</b> — stable operation, motion control and basic interaction demonstrated.</div></li>
<li><span class="t-when">2026-06-25</span><div class="t-what"><b>Working group formally established</b> — all four roles at the same table.</div></li>
<li><span class="t-when">2026-07</span><div class="t-what"><b>Joined the AGIROS ecosystem</b> — the ROS SIG keeps supplying packages.</div></li>
<li><span class="t-when">2026-10-18</span><div class="t-what"><b>RISC-V Summit China</b> — a small RISC-V biped running openKylin was demonstrated.</div></li>
</ul>

## Robot platforms: OpenLoong

OpenLoong is incubated by the OpenAtom Foundation and operated by Humanoid Robot (Shanghai) Co. It provides a complete open hardware family from full-size to teaching platforms:

| Platform | Positioning |
| --- | --- |
| Qinglong / Linglong | Full-size humanoid: 43 DoF, 182 cm, 75 kg |
| Qinglong Mini | Small reinforcement-learning platform |
| NanoLoong | Open-source biped teaching kit |

## Roadmap 1: openKylin ROS SIG

From “supplying packages” to “a robot reference system”. The first five items have already happened; the last two are planned.

<ul class="timeline">
<li><span class="t-when">2024-07</span><div class="t-what"><b>ROS SIG founded</b></div></li>
<li><span class="t-when">2025-11</span><div class="t-what"><b>Multi-architecture validation completed</b>; the robotics plan started in 2026-01.</div></li>
<li><span class="t-when">2026-02</span><div class="t-what"><b>100+ ROS packages packaged</b></div></li>
<li><span class="t-when">2026-08</span><div class="t-what"><b>Jazzy ros-base: 228 packages passed three local gates</b> (bootstrap build, rebuild with tests, install smoke test on a clean environment) and were pushed to OKBS for four-architecture builds.</div></li>
<li><span class="t-when">2026-10</span><div class="t-what"><b>ros-base 228/228 across four architectures (including riscv64) entered the 2.0 proposed repository and installs with apt</b>; jazzy desktop reached 59 packages ready; 3.0 Lyrical ros-base passed validation with 230 packages and a fully green CI.</div></li>
<li class="plan"><span class="t-when">2026-12 <span class="tag-plan">planned</span></span><div class="t-what">ros-base moves to the stable repository with the 2.0 release cadence; desktop is added incrementally (resolving CI and system-package dependencies); 3.0 ros-base finishes four-architecture builds.</div></li>
<li class="plan"><span class="t-when">2027 <span class="tag-plan">planned</span></span><div class="t-what">Nav2 / MoveIt packaged; RISC-V robot reference image; multi-platform regression on real hardware; openKylin robot edition released.</div></li>
</ul>

## Roadmap 2: the embodied intelligence working group

Turning “pluggable everywhere” into specifications, tests and reference hardware. All five steps are planned — **partners are welcome to claim one**.

<ul class="timeline">
<li class="plan"><span class="t-when">2026-Q4 <span class="tag-plan">planned</span></span><div class="t-what"><b>Open solution v0</b> — interface lists for the three layers, first compatibility matrix, K3 / Titan reference software stack.</div></li>
<li class="plan"><span class="t-when">2026-12 <span class="tag-plan">planned</span></span><div class="t-what"><b>Reference image v1</b> — dual-domain openKylin + ROS 2 + RT-Thread image, reproducible on K3 / A210 / Titan.</div></li>
<li class="plan"><span class="t-when">2027-Q1 <span class="tag-plan">planned</span></span><div class="t-what"><b>Compatibility test suite</b> — interface specs and conformance tests for the five pluggable points, CI regression on real hardware.</div></li>
<li class="plan"><span class="t-when">2027-Q2 <span class="tag-plan">planned</span></span><div class="t-what"><b>Second robot platform</b> — Qinglong Mini / NanoLoong teaching platform plus a university course kit.</div></li>
<li class="plan"><span class="t-when">2027-H2 <span class="tag-plan">planned</span></span><div class="t-what"><b>Scenario pilots and standardisation</b> — industrial / service reference robots; interface specs into community standards; compatibility matrix v2.</div></li>
</ul>

> **Provenance note:** items tagged “planned” are internal working-group plans subject to community decisions, not public commitments. Sources for the factual items are listed on the [sources & licensing]({{< relref "licensing.md" >}}) page.

## How the ecosystem lands in engineering terms

- **Software:** openKylin provides the RISC-V system and ROS package supply, the ROS SIG owns packaging and quality gates, and the working group owns the three-layer interfaces and the compatibility matrix.
- **Hardware:** OpenLoong provides full robots and open hardware so the interface list has real joints, buses and sensors to connect to.
- **Silicon:** SpacemiT, UltraRISC and Milk-V provide reference platforms so every layer has reproducible hardware underneath.
- **Verification:** Kubuds assembles the layers, runs end-to-end measurements and writes the results into the provenance notes on these pages.

<div class="cta-band" style="margin-top:2.2rem">
<div>
<h2>Your project can be the next stop on this line</h2>
<p>Package one missing library, connect a new robot platform, or run the conformance tests on your own hardware — all of it counts.</p>
</div>
<div><a class="btn" href="{{< relref "join.md" >}}">Join us →</a></div>
</div>
