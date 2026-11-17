# clash-rules

动态住宅 IP + 国外 AI 专属分流规则（Subconverter 远程配置）。

## 远程配置地址（Raw）

```text
https://raw.githubusercontent.com/zf158338-eng/clash-rules/main/ai-residential.ini
```

## 适用面板设置（edg / Subconverter）

- **订阅转换后端**：`https://SUBAPI.cmliussss.net`
- **订阅转换配置文件**：自定义 -> `https://raw.githubusercontent.com/zf158338-eng/clash-rules/main/ai-residential.ini`
- 勾选：`Emoji`、`TLS 1.3`、`基础节点排序`、`展开规则全文`

## 核心分组说明

- `🏠 住宅IP`（`url-test`）：通过通用正则自动收录节点名称中包含 `住宅 / 家宽 / 家宅 / 双ISP / 原生 / 静态 / ISP / Residential / Home` 的节点，即使 IP 经常变更也能自动归类；同时严格剔除香港（HK）、澳门（MO）、中国大陆（CN）、伊朗（IR）、俄罗斯（RU）、白俄罗斯（BY）、朝鲜（KP）、叙利亚（SY）、古巴（CU）及提示信息节点。
- `🤖 国外AI`（`select`）：默认优先使用 `🏠 住宅IP`，并把 OpenAI / ChatGPT / Claude / Gemini / Google AI Studio / Antigravity / Grok / Perplexity / Copilot / Cursor / OpenRouter 等规则置于微软、谷歌、媒体规则之前，确保所有国外 AI 流量稳定走非限区住宅 IP。
- `🌏 AI非限区备用`（`url-test`）：作为 `🤖 国外AI` 的备用池，同样严格屏蔽香港及受限地区节点。
- 其余地区与常见分流组（日/韩/狮城/美/港/台/其他、Telegram、YouTube、Netflix、国外媒体、B站、微软、苹果、游戏、直连、拦截、漏网之鱼）均采用通用正则动态匹配。
