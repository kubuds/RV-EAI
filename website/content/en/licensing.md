---
title: Sources & licensing
description: Where every pixel comes from — images, fonts, data provenance and licences. All diagrams are drawn in-house; no web fonts, no third-party photography.
lead: This page explains where every pixel on the site comes from. We deliberately use no third-party photography, product shots or logos, to stay clear of licensing risk.
---

## Images: all drawn in-house as SVG

Every graphic on this site is hand-written SVG produced for this project — no bitmaps, no screenshots, no vendor marketing imagery. Current inventory:

| Graphic | Where | Description | Licence |
| --- | --- | --- | --- |
| Humanoid cross-section with layer highlight | home | line drawing explaining the body / cerebellum / brain split | Apache-2.0 |
| Three time scales (μs / ms / 10 ms) | home hero | illustrative diagram of the three layers' time budgets | Apache-2.0 |
| Architecture overview (3 hardware + 4 software layers) | architecture | redrawn for the web from the released blueprint | Apache-2.0 |
| favicon and brand blocks | site-wide | geometric shapes | Apache-2.0 |

> The original deck contains on-site photographs and vendor-supplied figures (joint-motor diagrams, board photos, robot running shots). Copyright for those belongs to the respective vendors and communities, so **we do not reuse them here** and substitute self-drawn illustrations.

## Fonts: system stack only

The site loads no web fonts at all (no Google Fonts, no self-hosted woff), so no font licence is involved:

```
-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue",
"PingFang SC", "Hiragino Sans GB", "Microsoft YaHei",
"Source Han Sans SC", "Noto Sans CJK SC", sans-serif
ui-monospace, SFMono-Regular, Menlo, Consolas, "Liberation Mono", monospace
```

Rendering depends on the visitor's own operating system fonts: nothing is distributed, and no font licence fees arise.

## Trademarks

Names and part numbers appearing on this site — RISC-V, openKylin, OpenLoong, Milk-V, UltraRISC, SpacemiT, Zhihe Computing, Axera, Rockchip, HPMicro, GigaDevice, WCH, Espressif, RT-Thread, FlagOS, llama.cpp, TileLang, ROS 2 and others — are trademarks or product names of their respective owners, used only for factual reference and description. **No logos or visual identities are used.**

## Data provenance

Every number on the site carries a provenance tag, in four classes:

| Tag | Meaning | Example |
| --- | --- | --- |
| vendor data / vendor docs | from public vendor material, not independently re-measured here | K3 60 TOPS (INT4 sparse peak), HPM6E8Y 1 μs current loop |
| our measurement | measured by Kubuds on a K3 board (Bianbu 4.0.7 / kernel 6.18.3 / 2026-10-21), conditions stated | 1B VLM 24.09 t/s, 24B MoE 12.00 t/s, IME2 970 / 5632 GMAC/s |
| community & ecosystem | from open community progress and announcements | openKylin ROS SIG 228/228 packages in the repository, working group formed 2026-06-25 |
| planned | internal working-group plans, subject to community decisions | ROS SIG items after 2026-12, the five working-group steps |

Main public sources by category:

- **RISC-V industry:** riscv.org, NVIDIA blog (2024 RISC-V core shipments), Meta MTIA blog, Google Coral NPU developer blog, RISC-V Summit China 2025 (Krste Asanovic extension roadmap)
- **Silicon and boards:** SpacemiT (spacemit.com), Zhihe Computing (developer.zhcomputing.com), Milk-V (milkv.io), UltraRISC, Axera (axera-tech.com), Rockchip (rock-chips.com), HPMicro (hpmicro.com), GigaDevice (gigadevice.com), WCH (wch.cn), Espressif (espressif.com), Zhongke Benyuan
- **Community and ecosystem:** openKylin (including ROS SIG and embodied-AI working group announcements), OpenLoong project pages, AGIROS community, BAAI FlagOS, llama.cpp / TileLang / ncnn upstream repositories, ROS 2 documentation
- **Models:** BAAI RoboBrain 2.0, NVIDIA GR00T, Physical Intelligence π0.5, Qwen-VL and other public model pages

> The full source list (with item numbers, collection dates and open items) is maintained with the release material in the repository's `whitepapers/` directory and the `cite.txt` of the release package.

## Content licence

- Site text and in-house diagrams: **Apache-2.0** (see the repository `LICENSE`).
- Third-party data and names quoted here remain the property of their sources; they are used for factual reference only, with provenance class and source category stated.
- If you are a rights holder and consider a citation inappropriate, email [wuwei@rv2036.org](mailto:wuwei@rv2036.org) and we will act immediately.

## Policy for future third-party assets

Our internal rule is “register first, publish second”:

1. Record the **original URL + licence (SPDX identifier) + retrieval date** and list it on this page;
2. Prefer CC0 / CC-BY / clearly open-licensed assets, with attribution as required;
3. Vendor product images and on-site photographs need **written permission** (email is enough); otherwise use a self-drawn illustration;
4. Never publish images of unknown origin, never use vendor logos as decoration, never embed web fonts.
