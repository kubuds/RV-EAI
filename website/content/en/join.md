---
title: Join us
description: How to plug your silicon, robot platform or software into RV-EAI — four ways to take part, the claim list, the compatibility matrix and the ladder.
lead: The value of this solution depends on how many people plug in. Wherever you sit in the stack, if you can demonstrate one pluggable point, the result belongs in the matrix.
---

## Who we are looking for

<div class="grid-cards">
<div class="card">
<h3>Silicon and module vendors</h3>
<p>Bring your BSP, operator library and runtime into one layer: drives and FOC for the body, real-time cores and buses for the cerebellum, NPU / AI CPU and SDK for the brain.</p>
</div>
<div class="card">
<h3>Robot and hardware makers</h3>
<p>Provide joints, buses and sensor interfaces, and grow “reference hardware” from one machine into a family. After Qinglong Mini / NanoLoong we need more platforms.</p>
</div>
<div class="card">
<h3>Integrators and universities</h3>
<p>Run scenario pilots on the reference image, or build a course kit on this stack; universities can also claim part of the conformance testing.</p>
</div>
<div class="card">
<h3>Individual developers</h3>
<p>Get one model running, package one ROS library, fix one operator — all of it counts. The repository is open and results go into the matrix; we judge results, not employers.</p>
</div>
</div>

## Claim one of the five pluggable points

| Pluggable point | What you bring | What we do |
| --- | --- | --- |
| ① Body: motors & I/O | Drive / MCU / module BSP or datasheet, measurement on hardware | Integrate into reference hardware, record in the compatibility matrix |
| ② Cerebellum: real-time control | Real-time core and TCM specs, CAN-FD / EtherCAT interfaces, RTOS port | Adapt the dual-domain image, verify the millisecond loop |
| ③ Brain: AI compute | NPU / AI CPU specs, operator coverage list, inference SDK | Run local LLM / VLM / VLA, publish conditional measurements |
| ④ Operating system | RISC-V image of your distribution, ROS 2 package status | Add to the five-distribution matrix, run hardware regression |
| ⑤ AI framework & models | Runtime or model weights, adaptation notes | Add to one of the three framework routes, record usability |

> **The test is simple:** after swapping this one point, the other four need no change and the layer above needs no re-adaptation — that qualifies.

## The ladder

<ul class="timeline">
<li><span class="t-when">Step 1</span><div class="t-what"><b>Get it running</b> — bring your component up on the reference image, keep the logs and reproducible commands.</div></li>
<li><span class="t-when">Step 2</span><div class="t-what"><b>Submit the result</b> — record “part number + conditions + result” in the repository (conditions must be complete: build version, thread count, quantisation format).</div></li>
<li><span class="t-when">Step 3</span><div class="t-what"><b>Enter the matrix</b> — the working group reviews it and the combination becomes part of the public compatibility matrix.</div></li>
<li class="plan"><span class="t-when">Step 4 <span class="tag-plan">planned</span></span><div class="t-what"><b>Reference hardware / scenario pilot</b> — partners who can offer complete machines build industrial or service reference implementations with us.</div></li>
</ul>

## What you get

- **Interface lists:** the interfaces of the three hardware and four software layers, and the boundaries of the five pluggable points.
- **Reference images:** a dual-domain openKylin + ROS 2 + RT-Thread image, reproducible on K3 / A210 / Titan.
- **A measurement method:** how to measure, how to record conditions, how results are published — so no one argues about unmatched benchmarks.
- **Public credit:** every component in the matrix carries its part number and contributor; nobody is anonymised away.

## What we will not ask of you

- No exclusive licensing, and no giving up your own commercial edition;
- No forced convergence onto one framework or one chip — three framework routes coexisting is the point;
- No requirement to have a complete robot; one working pluggable point is enough to join.

## Contact

| Channel | Address |
| --- | --- |
| Email | [wuwei@rv2036.org](mailto:wuwei@rv2036.org) |
| Community | [rv2036.org](https://rv2036.org) · Jiachen Project · openKylin · FlagOS |
| Code and issues | [repository](https://github.com/kubuds/RV-EAI) |
| Recruiting | Jiachen Project · openKylin · FlagOS continuously recruit open-source interns and ecosystem partners |

<div class="cta-band" style="margin-top:2.2rem">
<div>
<h2>Let's build some fun robots together</h2>
<p>Bring your silicon, your robot or a piece of working code, and we will line up the interfaces.</p>
</div>
<div><a class="btn" href="mailto:wuwei@rv2036.org">Email us →</a></div>
</div>
