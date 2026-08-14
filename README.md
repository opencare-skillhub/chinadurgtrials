# china-drug-trials-skills

可独立部署的 WorkBuddy Skill：采集中国药物临床试验登记与信息公示平台记录，并输出原始 HTML、网页原样 Word 与 RAG JSON。

## 独立性

本目录不依赖父项目路径。所有可执行代码与依赖声明均在 `scripts/` 中：

```text
china-drug-trials-skills/
├── SKILL.md
├── README.md
├── scripts/
│   ├── scraper.py
│   ├── main.py
│   ├── cookie_tools.py
│   ├── build_json_from_raw.py
│   ├── config.example.json
│   └── requirements.txt
└── references/
    └── platform-workflow.md
```

## 作为 Skill 部署

将整个 `china-drug-trials-skills/` 目录复制到目标环境的 Skill 目录，或使用 `china-drug-trials-skills.zip` 安装。不要只复制 `SKILL.md`，脚本目录是完整工作流的一部分。

## 直接命令行使用

```bash
cd china-drug-trials-skills
python3 -m venv .venv
source .venv/bin/activate
pip install -r scripts/requirements.txt
cp scripts/config.example.json config.json
python3 scripts/main.py
```

`main.py` 会在当前目录读取/创建 `config.json`。其 Cookie 更新菜单支持粘贴浏览器 cURL 或 HTTP 响应头。

也可以直接运行：

```bash
python3 scripts/scraper.py --config config.json
python3 scripts/scraper.py --config config.json --incremental
```

## 安全与合规

- Cookie 仅保存在本地；不要提交、发送或打包真实 `config.json`。
- 仅处理有权访问的信息，遵守目标平台规则和适用要求。
- 保持合理请求间隔，不并发访问、不规避访问控制。

完整操作说明见 `SKILL.md`。
