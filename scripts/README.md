# 脚本

| 脚本 | 用途 |
| --- | --- |
| `check_links.py` | 站点内部链接检查：把构建产物里每个 `href`/`src` 映射到文件，列出不可达目标；`--live` 再对 `https://rv-eai.org` 逐条实测 HTTP 状态 |
| `check_i18n_links.py` | 语言切换器与 hreflang 检查：每个页面 × 每种语言的跳转目标必须在构建产物中存在 |

用法（先构建出 `website/public`）：

```bash
hugo --source website --gc --minify --baseURL "https://rv-eai.org/"
python3 scripts/check_links.py website/public
python3 scripts/check_links.py website/public --live
python3 scripts/check_i18n_links.py website/public
```

后续将加入：参考镜像构建脚本、可插拔点一致性测试、实测数据汇总（与 `src/` 配套）。
