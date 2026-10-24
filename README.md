# SLATE Teams 文档站

面向使用者的手册，中英成对。站点根就是仓库里的 `docs/`（GitHub Pages 认 main 分支的 `/docs`），
域名 `docs.teams.slate-ai.site`。产品仓库是 [SLATE_Teams](https://github.com/CaryWang1234/SLATE-Teams)，
门面（落地页 + 快速上手）在 [teams.slate-ai.site](https://teams.slate-ai.site/)。

## 怎么改

内容只有 Markdown，一份中文、一份英文，**文件名必须一致**——构建器按文件名配对，
缺任一侧就报错不出站。

```
content/zh/05-office.md      ←→   content/en/05-office.md
```

frontmatter 四项必填（`title` / `description` / `section` / `order`）；`order` 是全局排序，
同一章的两侧必须相同，`section` 用各自语言的措辞。站内链接写相对路径
（`./05-office.md#due`），构建器会按当前语言改写并核对锚点。

```
python build.py            # 生成到 docs/
python build.py --check    # 只校验：frontmatter、双语配对、站内链接与锚点
python build.py --clean    # 生成前清空 docs/
```

零依赖，只用 Python 标准库。`--check` 不过就不该提交产物。

## 排版能力

标题（自动进右侧目录）、表格、有序/无序嵌套列表、代码块（带复制）、
引用块、`:::note / :::tip / :::warning / :::danger` 提示框（可跟自定义标题）。

## 视觉口径

「席 · Ledger」：石墨纸面 + 红墨，直角、无投影、无渐变、无毛玻璃，数字走等宽。
令牌与产品、门面页同一套值，改颜色只改 `theme/docs.css` 的 `:root` 与
`html[data-theme="light"]` 两块，别在页面里写死色值。
