你是一个资深 DevOps + JavaScript/TypeScript 工程师，请帮我生成一个 GitHub Action 项目，名为 `feishu-action`，要求如下：

🔧 **项目功能需求**：
1. 当有人在 PR 上进行操作（创建、更新、合并）时，向指定的飞书群发送通知
2. 支持自定义通知模板、emoji 样式，并允许通过参数动态 @ 指定人员
3. 支持其他 GitHub 事件触发通知，如：
   - Push（包括 tag push）
   - Workflow run 成功或失败
   - Release 创建或发布
   - Issue 被创建或关闭
   - Branch 创建、评论被添加等其他常见事件（可自由扩展）
4. 要求支持多种通知风格（如工程风、可爱风、女黑客风、日系风），用户可通过参数切换风格
5. 要求支持通过 `config.yml` 文件集中管理多个事件和通知模板（提高复用性）

📦 **技术选型与项目结构**：
- 使用 **TypeScript** 编写，类型安全，代码可维护性高
- 使用 GitHub Actions Toolkit（@actions/core, @actions/github 等）
- 源码放在 `src/`，构建产物输出到 `dist/`，使用 `ncc` 打包（兼容 GitHub Actions）
- 项目结构清晰，使用模块化设计（如 `core/`, `utils/`, `notifier/` 等目录）
- 合理封装飞书通知逻辑、参数解析、模板渲染、GitHub 事件处理等功能模块

🧪 **测试与测试覆盖率**：
- 使用 [`jest`](https://jestjs.io/) 编写单元测试，结构清晰、可维护
- 集成 [`ts-jest`] 以支持 TypeScript 测试
- 使用 [`c8`](https://github.com/bcoe/c8) 或 [`nyc`](https://github.com/istanbuljs/nyc) 实现测试覆盖率统计
- 提供 `npm run test`、`npm run coverage` 脚本
- 要求代码覆盖率不低于 90%，并在 PR 检查中执行测试覆盖率校验

🧰 **版本管理与提交规范**：
- 所有提交必须符合 [Conventional Commits](https://www.conventionalcommits.org/) 规范
- 使用 `commitlint` + `husky` 实现提交检查
- 使用 `commitizen` 提供交互式提交命令（`npm run commit`）
- 使用 `standard-version` 管理语义版本、生成 changelog、自动 tag
- `.versionrc` 自定义 release 配置
- `CHANGELOG.md` 自动生成并更新
- 可选：配合 GitHub Actions 实现自动 release（tag 发布后自动生成 GitHub Release）

📚 **文档自动化与开发者友好性**：
- 使用 [`typedoc`](https://typedoc.org/) 自动从 TypeScript 注释生成 API 文档
- 在 `docs/` 目录输出 HTML 文档，并在 `README.md` 中加入链接
- README 包含完整的使用示例、输入输出说明、模板配置说明、常见问题等
- 项目应包含徽章（构建状态、测试覆盖率、版本、License 等）

💥 **错误处理与健壮性**：
- 所有核心逻辑都必须有明确的错误处理机制（try/catch + 错误日志）
- 对无效配置、飞书 webhook 请求失败、GitHub API 错误等必须有详细提示
- 在用户配置错误时提供合理 fallback 或中断提示
- 建议使用自定义错误类，如 `ConfigError`, `NotifyError`, `TemplateError` 等统一管理错误处理

📤 **发布与部署**：
- 提供发布到 GitHub Marketplace 的说明
- 每次发布 tag 时自动构建产物、生成 changelog、发布 GitHub Release
- 生成后的 `dist/` 目录仅包含打包后的运行时代码（不含源码）

🌐 **国际化（i18n）支持**：
- 所有用户可见的通知文本需支持国际化，至少支持中英文切换
- 文本内容应从国际化词库中读取，而非硬编码字符串
- 使用简单的 JSON 文件存储语言包，如 `locales/zh-CN.json`、`locales/en-US.json`
- 语言通过 `config.yml` 中配置，如：`language: zh-CN`
- 模板中使用占位符（如 `{{ pr.title }}`）自动填入上下文，支持多语言渲染
- 用户可自定义语言包并覆盖默认内容

🛠️ **项目开发脚本（`package.json`）应包含**：
- `npm run dev`：开发模式运行，支持实时调试
- `npm run build`：使用 `ncc` 构建 dist
- `npm run test`：运行所有测试
- `npm run coverage`：输出覆盖率报告
- `npm run commit`：交互式 commitizen 提交
- `npm run release`：standard-version 生成版本和日志
- `npm run docs`：生成 API 文档

请根据上述完整要求，生成一个结构完整、代码清晰、模块化、具备测试与文档支持的 GitHub Action 项目，并使用最符合开源软件开发最佳实践的方式组织代码和文档。
