# Spring Breeze 项目说明

Spring Breeze 是 chifanjie 开发的 AI 热点监控工具，用于围绕关键词自动聚合公开信息源内容，并通过 AI 进行相关性判断、真实性初筛、重要性分级和摘要整理。

## 核心功能

- 关键词管理：添加、启用、暂停和删除监控词。
- 热点聚合：从搜索引擎、内容平台和社交平台收集相关内容。
- AI 分析：识别内容与关键词的相关性，生成摘要和重要性等级。
- 实时推送：通过 WebSocket 将新热点推送到浏览器。
- 邮件通知：可选 SMTP 配置，用于高优先级提醒。
- 本地持久化：使用 SQLite + Prisma 存储关键词、热点、通知和设置。

## 技术栈

| 层级 | 技术 | 说明 |
|------|------|------|
| 前端 | React + Vite + Tailwind CSS | 白底高级感工作台界面 |
| 后端 | Node.js + Express | API 服务和任务调度 |
| 数据库 | SQLite + Prisma | 本地轻量存储 |
| AI 服务 | OpenRouter API | 内容分析和摘要 |
| 定时任务 | node-cron | 周期性热点检查 |
| 实时通信 | Socket.io | 浏览器实时推送 |
| 邮件 | Nodemailer | 邮件通知 |

## 项目结构

```text
spring_breeze/
├── client/                  # 前端应用
├── server/                  # 后端服务
│   ├── prisma/              # Prisma schema
│   └── src/                 # API、服务、任务、测试
├── docs/                    # 文档
└── skills/                  # Agent Skills
```

## 快速开始

```bash
git clone https://github.com/chifanjie/spring_breeze.git
cd spring_breeze

cd server
npm install
npx prisma generate
npx prisma db push
npm run dev
```

另开一个终端：

```bash
cd client
npm install
npm run dev
```

访问 `http://localhost:5173` 使用前端页面。
