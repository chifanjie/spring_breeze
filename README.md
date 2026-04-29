# Spring Breeze

> 作者：chifanjie

Spring Breeze 是一个面向热点追踪和信息筛选的 AI 监控工具。它可以围绕用户配置的关键词，自动从多个公开信息源抓取相关内容，并使用 AI 完成相关性判断、真实性初筛、重要性分级和摘要整理，帮助用户更快发现值得关注的信息。

项目包含完整的前后端实现：前端提供轻量、清爽的热点工作台；后端负责关键词管理、定时抓取、AI 分析、数据存储、实时推送和邮件通知。适合用于技术热点监控、产品情报收集、内容选题辅助和个人信息雷达。

## 功能特性

- 关键词监控：支持添加、启用、暂停和删除监控词。
- 多源热点聚合：支持从搜索引擎、社交平台和内容平台聚合信息。
- AI 内容分析：通过 OpenRouter 对内容进行相关性、可信度、重要性和摘要分析。
- 热点筛选排序：按来源、等级、关键词、时间范围、相关性和热度排序。
- 实时通知：通过 Socket.io 推送新热点，可选邮件提醒。
- 本地数据存储：使用 SQLite + Prisma，便于本地运行和迁移。
- Agent Skill：保留可供 AI 编程工具调用的热点监控技能包。

## 技术栈

| 模块 | 技术 |
|------|------|
| 前端 | React 19, Vite, TypeScript, Tailwind CSS, Framer Motion |
| 后端 | Node.js, Express 5, TypeScript |
| 数据库 | SQLite, Prisma |
| 实时通信 | Socket.io |
| AI 分析 | OpenRouter |
| 定时任务 | node-cron |
| 邮件通知 | Nodemailer |

## 项目结构

```text
spring_breeze/
├── client/                  # 前端应用
├── server/                  # 后端服务
│   ├── prisma/              # Prisma schema 和本地 SQLite 数据库
│   └── src/                 # API、服务、定时任务和测试
├── docs/                    # 项目文档
└── skills/                  # Agent Skills
```

## 快速运行

### 前置条件

- Node.js 18 或更高版本，推荐 Node.js 20 LTS
- OpenRouter API Key，用于 AI 分析
- Twitter API Key，可选，用于抓取 Twitter/X 数据

### 1. 克隆项目

```bash
git clone https://github.com/chifanjie/spring_breeze.git
cd spring_breeze
```

### 2. 安装后端依赖并初始化数据库

```bash
cd server
npm install
npx prisma generate
npx prisma db push
```

### 3. 安装前端依赖

```bash
cd ../client
npm install
```

### 4. 配置环境变量

```bash
cp server/.env.example server/.env
```

编辑 `server/.env`：

```env
DATABASE_URL="file:./dev.db"
PORT=3001
CLIENT_URL=http://localhost:5173

OPENROUTER_API_KEY=your_openrouter_api_key
TWITTER_API_KEY=your_twitter_api_key
```

### 5. 启动服务

打开两个终端：

```bash
# 终端 1：后端
cd server
npm run dev
```

```bash
# 终端 2：前端
cd client
npm run dev
```

访问：

| 服务 | 地址 |
|------|------|
| 前端页面 | http://localhost:5173 |
| 后端 API | http://localhost:3001 |
| Prisma Studio | http://localhost:5555 |

## 使用方式

1. 打开前端页面。
2. 在“监控词”中添加要追踪的关键词。
3. 回到“热点雷达”，点击“立即扫描”，或等待定时任务自动扫描。
4. 使用筛选和排序工具查看不同来源、等级和时间范围的热点。

## 说明

- `.env`、本地数据库、依赖目录和构建产物已被 `.gitignore` 排除，不会提交到仓库。
- 如果热点为空，通常是还没有添加启用的监控词，或 API Key / 网络环境不可用。
- 更详细的本地运行步骤见 [docs/LOCAL_SETUP.md](docs/LOCAL_SETUP.md)。
