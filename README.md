# TryAllAPI × WorkBuddy

> **Product README (standalone):** [xianyu110/tryallapi](https://github.com/xianyu110/tryallapi) — this repo is only the WorkBuddy integration guide, not the primary TryAllAPI product page.


**Product:** [TryAllAPI](https://tryallapi.com/) (on-site brand: MomoAPI / momoAPIPro) — multi-model AI API gateway.  
**Base URL (OpenAI-compatible):** `https://tryallapi.com/v1`  
**Pricing:** USD pay-as-you-go (top-up from ~$1; official list price × group multiplier). See [pricing](https://tryallapi.com/pricing).  
**Docs:** [docs.tryallapi.com](https://docs.tryallapi.com/) · [Apifox](https://5oq7d57fbk.apifox.cn)  
**Contact:** bgnwd15@gmail.com  

> Third-party aggregator — **not** affiliated with OpenAI, Anthropic, or Google. **Never commit API keys.** Model count and prices change; trust the live console.

This repo is a short guide: wire TryAllAPI into WorkBuddy with one Key.

---

# WorkBuddy 接入 tryallapi：一个 Key 用遍 GPT-6、Claude、Gemini，3 分钟配好

WorkBuddy 好用，但默认模型总有不够用的时候：想让 Claude 写代码、Gemini 看图、GPT-6 做长推理，一家一家去开账号、绑海外卡、管一堆 Key，光折腾就把干活的心气耗没了。

其实 WorkBuddy 留了个口子，**自定义模型**。只要是 OpenAI 兼容协议的接口都能接进来。这篇就用 [tryallapi](https://tryallapi.com/) 演示：一个 Key、一个地址，370 个模型随便切。

## 一、tryallapi 是什么

tryallapi（momoAPIPro）是一个 AI 接口聚合平台，**完全兼容 OpenAI 协议**，按量计费、明码实价。官网写的是「10 万+客户的选择，18 个月稳定运营」。

![tryallapi 首页](https://upload.maynor1024.live/file/1790852752397_01-home.png)

对 WorkBuddy 用户来说，最关键的有三点：

- **一个地址通吃**：Base URL 是 `https://tryallapi.com/v1`，所有模型共用，换模型只改模型名。
- **模型全**：模型广场目前上架 370 个，OpenAI 85 个、Google 30 个、Anthropic 15 个、Grok 14 个，DeepSeek、Kimi、GLM、Qwen 也都有，还有生图、视频、音乐模型。
- **门槛低**：最低充 $1 起，微信、支付宝、银行卡都能付，大额充值还有折扣。

![平台特性](https://upload.maynor1024.live/file/1790852755858_02-home-features.png)

![模型广场：370 个模型](https://upload.maynor1024.live/file/1790852755498_03-pricing-model-list.png)

## 二、第一步：注册并创建 API Key

1. 打开 [tryallapi.com](https://tryallapi.com/) 注册账号并登录。
2. 进入**控制台**，充值一点额度（$1 就能先试）。
3. 在控制台的令牌（API Key）页面新建一个 Key，复制保存好。

> Key 相当于你的钱包密码，别发群里、别贴进公开仓库。

## 三、第二步：在 WorkBuddy 里添加模型

打开 WorkBuddy，依次点 **设置 → 模型 → 自定义模型 → + 添加模型**，会弹出下面这个窗口（右上角标着「仅支持 OpenAI 兼容协议 API」，tryallapi 正好满足）：

![WorkBuddy 添加模型](https://upload.maynor1024.live/file/1790852762871_07-wb-add.png)

按下面填：

| 字段 | 填什么 |
|---|---|
| 提供商 | 自定义 / Custom |
| 接口地址 | `https://tryallapi.com/v1/chat/completions` |
| API Key | 上一步复制的 Key |
| 模型名称 | 例如 `gemini-3.8-flash`（以模型广场显示的名称为准） |

**高级配置**按模型能力勾选：

- **工具调用**：WorkBuddy 要调工具、跑智能体任务，建议勾上。
- **图片输入**：模型支持看图才勾，比如 Gemini、GPT-6、Claude 系列。
- **推理模式**：用推理类模型时再开。
- **输入 / 输出**：上下文长度。Gemini 3.8 Flash 可以选输入 128K（131072）、输出 64K（65536）。

填好大概长这样：

![WorkBuddy 填写示例](https://upload.maynor1024.live/file/1790852765270_08-wb-filled.png)

点**保存**，回到对话框，在模型列表里选中刚加的模型，就能直接开聊了。

想多接几个模型？再点一次「添加模型」，接口地址和 Key 不变，只换模型名称就行。

## 四、推荐几个模型（附价格）

下面是模型广场默认展示的价格，单位是美元 / 百万 tokens，实际以官网为准：

| 模型 | 适合干什么 | 输入 | 输出 |
|---|---|---|---|
| `gemini-3.8-flash` | 日常主力、看图、长文，便宜又快 | $0.1103 | $0.5515 |
| `gpt-6-sol` / `gpt-6.1-sol` | 综合能力强，性价比高 | $0.1471 | $0.7354 |
| `gpt-6-luna` | 轻量任务、批量处理，几乎不花钱 | $0.0073 | $0.0368 |
| `gpt-5.6-sol` | 稳定的老将，写作和代码都行 | $0.3677 | $2.2060 |
| `claude-opus-5-5` | 写代码、复杂长任务 | $0.7059 | $3.5300 |
| `gpt-6-astra` | 旗舰级推理、硬骨头任务 | $0.7354 | $3.6770 |

![GPT-6 系列价格](https://upload.maynor1024.live/file/1790852761519_04-pricing-gpt-6.png)

![Claude 系列](https://upload.maynor1024.live/file/1790852755780_05-pricing-claude.png)

我的建议：**日常挂 Gemini 3.8 Flash 或 GPT-6 Sol，碰到难题再切 Claude Opus 或 GPT-6 Astra。** 钱花在刀刃上。

## 五、踩坑提醒

1. **接口地址要写全**。WorkBuddy 这里要填完整的 `https://tryallapi.com/v1/chat/completions`，只写到 `/v1` 可能连不上。
2. **模型名一个字母都不能错**。直接从模型广场复制，大小写和横杠都要一致。
3. **图片输入别乱勾**。纯文本模型勾了图片输入，传图时会报错。
4. **上下文别超上限**。输入、输出长度按模型实际支持的来设，设太大可能请求失败。
5. **报错先查余额和 Key**。401 多半是 Key 填错，额度不足会直接拒绝请求。

## 写在最后

WorkBuddy 负责干活，tryallapi 负责供“脑子”。一个 Key 把 GPT-6、Claude、Gemini 全装进去，想用谁切谁，不用再为每家模型单独折腾。

👉 立即注册：[tryallapi.com](https://tryallapi.com/)
📖 接口文档：[tryallapi 文档](https://5oq7d57fbk.apifox.cn)
💬 有问题可以加客服 QQ：1002569303
