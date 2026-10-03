# 智能面试系统

一个面向求职者的 AI 面试辅助平台。系统覆盖简历解析与评估、文字与语音模拟面试、面试日程、知识库问答和题库面试，帮助用户将准备、练习、复盘集中在同一个工作台中。

## 主要能力

- 简历管理：上传 PDF、Word、TXT 简历，异步解析、AI 评估并导出报告。
- 模拟面试：按技术方向、岗位描述和难度生成问题，支持多轮追问、作答记录和综合评价。
- 语音面试：通过 WebSocket 提供实时字幕、语音识别、语音合成和会话状态控制。
- 面试安排：解析面试邀请，提供日历视图、提醒和面试状态管理。
- 知识库：上传文档后自动分块与向量化，支持检索增强问答、题目生成、题库管理和专项面试。
- 模型配置：支持 DashScope、LM Studio、Kimi、DeepSeek、GLM 等 OpenAI 兼容模型提供方。

## 技术栈

| 层级 | 技术 |
| --- | --- |
| 后端 | Java 25、Spring Boot 4、Spring AI、Gradle |
| 前端 | React 18、TypeScript、Vite、Tailwind CSS |
| 数据与缓存 | PostgreSQL + pgvector、Redis + Redisson |
| 异步与存储 | Redis Stream、S3 兼容对象存储、Apache Tika |
| 其他 | WebSocket、SSE、Docker Compose、OpenAPI |

## 项目结构

```text
.
├── app/                    # Spring Boot 后端
│   └── src/main/
│       ├── java/           # 业务模块、通用能力与基础设施
│       └── resources/      # 配置、数据库迁移、提示词与面试技能
├── frontend/               # React 前端
│   └── src/                # 页面、组件、接口与类型定义
├── docker/                 # PostgreSQL 初始化等容器资源
├── docker-compose.yml      # 完整容器化部署
└── docker-compose.dev.yml  # 本地依赖服务
```

## 环境要求

- JDK 25
- Node.js 20+ 与 pnpm（或 npm）
- Docker Desktop（推荐，用于 PostgreSQL、Redis 和对象存储）

## 快速开始

### 1. 配置环境变量

复制示例文件并填写所需的模型服务密钥。请只在本机保存 `.env`，不要提交它。

```bash
cp .env.example .env
```

Windows PowerShell 可使用：

```powershell
Copy-Item .env.example .env
```

至少需要为准备使用的模型提供方填写 API Key，例如 `AI_BAILIAN_API_KEY`。数据库、Redis 和对象存储配置均可通过 `.env` 覆盖。

### 2. 启动基础服务

```bash
docker compose -f docker-compose.dev.yml up -d
```

### 3. 启动后端

```bash
./gradlew :app:bootRun
```

Windows：

```powershell
.\gradlew.bat :app:bootRun
```

后端默认运行在 `http://localhost:8080`，接口文档地址为 `http://localhost:8080/swagger-ui.html`。

### 4. 启动前端

```bash
cd frontend
pnpm install
pnpm run dev
```

前端默认地址为 `http://localhost:5173`。

## 常用命令

```bash
# 后端编译与测试
./gradlew :app:compileJava
./gradlew :app:test --no-daemon

# 前端构建
cd frontend && pnpm run build

# 启动开发依赖
docker compose -f docker-compose.dev.yml up -d
```

## 配置与安全

- 真实密钥、证书、环境变量文件和本地凭据仅应保存在本机。
- 模型文件、数据集、用户上传文件、运行时数据和本地数据库已由 `.gitignore` 排除。
- `application.yml` 中的默认数据库密码只用于本地开发示例；部署前必须用环境变量替换。
- 请勿将包含简历、面试记录或知识库原文的目录提交到公开仓库。

## 许可证

本项目沿用仓库中的 [LICENSE](LICENSE) 许可证。使用前请确认其条款符合你的发布和使用场景。
