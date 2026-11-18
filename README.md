# clash-rules

动态住宅 IP + 国外 AI 专属分流 + 强化绕过国内直连规则（Subconverter 远程配置）。

## 远程配置地址（Raw）

```text
https://raw.githubusercontent.com/zf158338-eng/clash-rules/main/ai-residential.ini
```

## 适用面板设置（edg / Subconverter）

- **订阅转换后端**：`https://SUBAPI.cmliussss.net`
- **订阅转换配置文件**：自定义 -> `https://raw.githubusercontent.com/zf158338-eng/clash-rules/main/ai-residential.ini`
- 勾选：`Emoji`、`TLS 1.3`、`基础节点排序`、`展开规则全文`

## 核心设计说明

- `🏠 住宅IP`（`url-test`）：通过通用正则自动收录 `住宅 / 家宽 / 家宅 / 双ISP / 原生 / 静态 / ISP / Residential / Home` 节点，同时严格剔除香港（HK）、澳门（MO）、中国大陆（CN）、伊朗（IR）、俄罗斯（RU）、白俄罗斯（BY）、朝鲜（KP）、叙利亚（SY）、古巴（CU）及提示信息节点。
- `🤖 国外AI`（`select`）：默认优先使用 `🏠 住宅IP`，并把 AI 规则置于微软、谷歌、媒体规则之前，禁止香港及受限地区节点进入。
- **强化国内直连与防误切**：
  - `🎯 全球直连` 锁定为仅 `DIRECT`，防止客户端缓存或误触将直连流量发往海外代理。
  - 接入 `rules/DirectCN.list` + `blackmatrix7/ChinaMedia.list` + `blackmatrix7/China.list` 并置于 `ProxyGFWlist` / `ProxyMedia` 之前，确保 `.cn` 全域名、国内 IP 测速站（`ip138.com` / `ipip.net` / `cip.cc` / `itdog.cn` / `speedtest.cn`）与国内主流视频 CDN（B站、抖音、快手、小红书、爱奇艺、优酷、腾讯视频、芒果TV）全速直连；同时保留 `ip.sb` / `ipinfo.io` / `ping0.cc` 走代理方便检测代理纯净度。
