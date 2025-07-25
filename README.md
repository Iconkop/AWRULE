# 🧱 AWAvenue Ads Rule Auto Sync

🔄 自动同步 [AWAvenue 广告规则](https://github.com/TG-Twilight/AWAvenue-Ads-Rule) 并发布为 Clash 格式规则文件。支持定时检查、版本发布和 Telegram 通知。

---

## 💡 项目亮点

- ⏰ **自动更新**：每小时自动检测上游是否有更新；
- 🧠 **智能跳过**：如上游规则未变更则跳过无效构建；
- 🛠 **手动触发强制构建**：无需等待定时；
- 🌏 **北京时间戳**：所有时间使用 Asia/Shanghai；
- 🔄 **自动提交、打 tag、发布 release**；
- 📢 **Telegram 双重通知**：文本 + 附件；
- 🧪 **可本地调试脚本**，轻松自定义。

---

## ⚙️ 工作流结构图

```text
               ┌──────────────────────────────┐
               │  触发方式                    │
               │  ┌─────────────┐             │
               │  │ 定时触发    │────────┐    │
               │  │ 每小时运行  │        │    │
               │  └─────────────┘        ▼    │
               │  ┌─────────────┐    [检查上游是否更新]
               │  │ 手动触发    │─────────────┘
               │  └─────────────┘
               └──────────────────────────────┘
                            │
                            ▼
                 [convert_rule.py 脚本转换]
                            │
                            ▼
                     [是否有文件更改？]
                            │
                      ┌─────┴─────┐
                  是 ─┤ 提交+发布 │
                      └─────┬─────┘
                            ▼
                  [Telegram 通知发送]

```

---

## 🧩 规则结构说明

本项目使用 Clash 的 `.list` 格式，支持通过自定义转换脚本将 YAML 源文件转为纯文本格式。

转换脚本路径：`scripts/convert_rule.py`

> 示例转换内容：

```
||example.com^
||ads.domain.net^
! 这是注释行
```

## 📄 规则文件地址

| 类型       | 说明                    | 链接地址 |
|------------|-------------------------|----------|
| 原始链接   | GitHub RAW 实时内容     | [`raw.githubusercontent.com`](https://raw.githubusercontent.com/Iconkop/awrule/main/AWAvenue-Ads-Rule-Clash-Classical.list) |
| 加速链接   | jsDelivr CDN（国内推荐）| [`cdn.jsdelivr.net`](https://cdn.jsdelivr.net/gh/Iconkop/awrule@main/AWAvenue-Ads-Rule-Clash-Classical.list) |

---

## 🧪 本地测试方法

你可以在本地手动测试转换逻辑：

### 1. 克隆本仓库

```bash
git clone https://github.com/Iconkop/awrule.git
cd awrule
```

### 2. 安装依赖

```bash
pip install -r requirements.txt
```

> 如无 `requirements.txt`，你可能只需要：

```bash
pip install requests
```

### 3. 手动运行转换脚本

```bash
python scripts/convert_rule.py
```

转换后的结果应输出至：

```
AWAvenue-Ads-Rule-Clash-Classical.list
```

---

## 🧪 测试自动流程（Actions）

- 推送任何更改（如规则、脚本）将触发构建；
- 你也可以手动进入 **Actions > update-rule.yml > Run workflow**，选择 `main` 分支触发。

---

## 📁 文件结构说明

```
.
├── .github/
│   └── workflows/
│       └── update-rule.yml       # 自动工作流配置
├── scripts/
│   ├── convert_rule.py           # 规则转换脚本
│   └── .last_hash                # 上次记录的 SHA 值缓存
├── AWAvenue-Ads-Rule-Clash-Classical.list  # 输出规则文件
├── README.md
```

---

## 🛡 常见问题 FAQ

### Q: 为什么有时候 workflow 不触发发布？

- A: 因为是定时任务触发时，会检测上游 SHA 值是否变化，只有变更时才继续执行转换和发布；
- 手动运行则**始终**执行全部流程，无视是否有变更。

### Q: 如何自定义规则格式？

编辑 `scripts/convert_rule.py` 文件，改写输出逻辑。例如支持 YAML/Surge/Stash 可在脚本中加分支。

---

## 📢 Telegram 通知设置

需要在仓库 Secrets 中配置以下环境变量：

| Secret 名称           | 含义                           |
|------------------------|--------------------------------|
| `TELEGRAM_BOT_TOKEN`   | 你的 Telegram Bot API Token     |
| `TELEGRAM_CHAT_ID`     | 接收通知的频道或用户 ID         |

通知包括：

- HTML 格式文字预览
- 附件 `.list` 文件发送

---

## ✅ 发布命名规范

自动打标签格式如下：

```text
v2025.07.24.1030
```

> 使用 `Asia/Shanghai` 北京时间生成。

---

## 🔗 相关链接

- 🔍 上游规则仓库：[TG-Twilight/AWAvenue-Ads-Rule](https://github.com/TG-Twilight/AWAvenue-Ads-Rule)
- 📄 本项目规则地址：[规则 RAW 文件](https://raw.githubusercontent.com/Iconkop/awrule/main/AWAvenue-Ads-Rule-Clash-Classical.list)
- 🚀 [GitHub Releases](https://github.com/Iconkop/awrule/releases)

---

## 🙏 致谢

- [TG-Twilight](https://github.com/TG-Twilight)
- [softprops/action-gh-release](https://github.com/softprops/action-gh-release)
- 所有开源贡献者 ❤️

---

## 📜 License

[MIT License](LICENSE)