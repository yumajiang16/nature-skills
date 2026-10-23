# Codex 项目级技能

在 Codex 网页版选择此仓库并启动新任务。项目入口位于
`.agents/skills/`，通过 Git 保存的相对符号链接指向 `../../skills/<name>`。
无需全局复制，也无需启动后台服务。旧对话的技能目录可能不会自动刷新；
配置提交后请在包含该提交的新任务中使用。

| 技能 | 用途 | 调用示例 |
| --- | --- | --- |
| nature-figure | 科研绘图、图件审计 | 使用 $nature-figure，以 Python 根据这些数据绘图 |
| nature-polishing | 润色、翻译已有文字 | 使用 $nature-polishing 润色以下摘要 |
| nature-writing | 根据证据起草、重构论文 | 使用 $nature-writing，根据这些结果起草 Discussion |
| nature-citation | 查找并验证 Nature/CNS 支撑引用 | 使用 $nature-citation，为这段文字补充 Nature 系列引用 |

同时保留 `nature-shared`，以支持相邻路径下的共享规范和期刊格式。
现有仓库插件可能把技能显示为 `nature-skills:nature-figure` 等带命名空间的
名称；可使用技能选择器中的完整名称，或明确说“使用 nature-figure”。

## Python 运行条件

写作和润色的指令路由不需要 Python 或 API key。绘图的 Python 路线及
引用脚本可按以下方式安装；所有命令从仓库根目录执行：

```bash
python3 -m venv /workspace/.venvs/nature-skills
source /workspace/.venvs/nature-skills/bin/activate
python -m pip install -c .github/requirements-ci.txt pytest pyyaml matplotlib seaborn pandas defusedxml -r skills/nature-figure/requirements.txt
python -m pip check
python .agents/skills/nature-citation/scripts/nature_citation.py --help
python -m pytest -q skills/nature-figure/tests skills/nature-citation/tests skills/nature-shared/tests
python -m pytest -q scripts/tests
```

其他机器可将虚拟环境路径替换为本机可写目录。不要把虚拟环境提交进 Git。
图件输出应放在 `output/` 或任务产物目录。

R 绘图路线需另外安装 R 及对应 ggplot2 等包，本次未配置或验证。
LaTeX 排版和 OpenRouter 图像生成也属于可选路线，分别需要 LaTeX 或对应
API 配置。不要将凭据写入仓库。

在线引用查询需要访问 `api.crossref.org` 和 `eutils.ncbi.nlm.nih.gov`；
阅读出版商原文还需目标出版商域名。离线测试通过不代表在线访问已授权，
也不代表每条候选文献已完成证据核验。

本次 Crossref 和 PubMed 的实际请求均遭代理 `403 Forbidden` 拒绝。
这两个域名已加入云环境配置草稿；需在环境设置中保存并发布，生效后重新
验证在线请求。该草稿不会随 Git 提交自动发布。

## 验证范围

已通过 Codex 0.163.0 app-server 的 `skills/list` 实际发现检查：四个主技能
及共享包均为 `scope: repo`、`enabled: true`，且没有解析错误。
这验证项目注册与可加载入口；网页版会话中的实际模型调用仍需在新任务中
验证，不能用本机发现检查替代。

本次工具测试为 48 项通过；仓库内容契约为 163 项及 16 个子测试通过。
`pip check`、仓库校验与技能元数据校验均通过。
