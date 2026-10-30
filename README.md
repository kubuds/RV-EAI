# RV-EAI

RISC-V-Based Open Solution for Embodied AI（RV-EAI）
基于 RISC-V 的具身智能开放解决方案。

官方网站 <https://rv-eai.org> 的源码仓库。

## 目录结构

| 目录 | 内容 | 状态 |
| --- | --- | --- |
| [`website/`](website/) | 官网源码（Hugo，中文 / English，明暗双配色） | 已上线内容 |
| `whitepapers/` | 白皮书与发布材料的可公开版本（PDF / Markdown） | 规划中 |
| `scripts/` | 站点构建、链接检查、数据同步等脚本 | 已有链接检查脚本 |
| `src/` | 参考实现代码、示例工程 | 规划中 |
| `3rd-party/` | 第三方素材登记（字体、图片、数据集）与其许可证说明 | 规划中 |

> **素材合规原则（对 `3rd-party/` 的硬性要求）**：任何引入的第三方素材必须在
> `3rd-party/README.md` 与站点「来源与许可」页同时登记 **原始 URL + 许可证（SPDX）+ 抓取日期**。
> 未登记的素材不得进入主分支。站点当前**不使用任何第三方图片与网络字体**，图表全部自绘 SVG。

## 本地构建站点

```bash
# 需要 Hugo extended >= 0.146（CI 固定 0.147.9）
hugo --source website --gc --minify --baseURL "https://rv-eai.org/"
# 产物在 website/public/
```

本地预览：

```bash
hugo server --source website -D
```

## 检查

```bash
python3 scripts/check_links.py website/public            # 站内链接可达性
python3 scripts/check_links.py website/public --live     # 再对线上逐条实测
python3 scripts/check_i18n_links.py website/public       # 语言切换 / hreflang 目标
```

## 部署

推送到 **`master` 或 `main`** 分支后，GitHub Actions（`.github/workflows/pages.yml`）会构建 `website/` 并发布到 GitHub Pages。
内部 GitLab 仓库默认分支是 `master`，GitHub 镜像 `kubuds/RV-EAI` 的默认分支也是 `master`，`main` 仅为兼容保留——
两个分支都会触发构建。也可以在 Actions → **Deploy website** → **Run workflow** 手动触发。

首次启用需要在仓库 Settings → Pages 把 **Source** 设为 **GitHub Actions**（不能选 "Deploy from a branch"），
自定义域名设为 `rv-eai.org`（DNS 侧 `rv-eai.org` 与 `www.rv-eai.org` 指向 `<org>.github.io`）。
未配置域名前会先跑在 `https://<org>.github.io/RV-EAI/`，workflow 用 `configure-pages` 输出的 `base_url` 自动适配子路径。

## 数据口径

站点上的每个数字都带口径标记（厂商数据 / 本团队实测 / 社区材料 / 规划），
完整来源与许可证说明见 <https://rv-eai.org/licensing/>。

## 许可证

- 代码与站点内容：Apache-2.0（见 [LICENSE](LICENSE)）。
- 文中提及的芯片、操作系统与产品名称归各自所有者所有。
