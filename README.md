# 财务管理系统 (内测版本 V0.1)

> **内测版本公告**：这是财务管理系统第一个内测版本（V0.1），目前处于功能验证阶段。欢迎测试并提供反馈，请勿用于生产环境。

一个本地部署的财务管理系统，支持多用户认证、交易管理、分类管理、数据分析图表。采用 Node.js + Express + SQLite 后端，以及 JavaScript + Bootstrap 5 + Chart.js 前端。

**版本状态**：`0.1.0-beta` | **发布日期**：2025-12-27 | **目标用户**：计算机知识匮乏人群

## 主要功能

- **用户认证**：注册、登录、JWT 令牌管理
- **交易管理**：添加、编辑、删除、查看交易记录
- **分类管理**：自定义收入和支出分类
- **数据分析**：月度统计、分类占比、趋势图表
- **数据导出**：支持导出为 Excel 和 PDF 格式
- **一键安装**：提供 Windows 可执行文件，无需安装 Node.js
- **高扩展架构**：仓库模式支持未来迁移到 PostgreSQL

## 快速开始

### 前提条件

- Node.js 18 或更高版本（仅开发需要）
- npm 或 yarn

### 安装步骤

1. 克隆或下载本项目。
2. 进入项目目录：
   ```bash
   cd finance-management-system
   ```
3. 安装依赖：
   ```bash
   npm install
   ```
4. 复制环境变量文件：
   ```bash
   cp .env.example .env
   ```
5. 编辑 `.env` 文件，设置 `JWT_SECRET` 等参数（可选）。
6. 初始化数据库：
   ```bash
   npm run migrate
   ```
7. 启动服务器：
   ```bash
   npm start
   ```
   或者直接运行 `start.bat`（Windows）。

8. 访问 `http://localhost:3000`。

### 一键启动（Windows）

项目提供了 `start.bat` 脚本，可自动检查环境、安装依赖、初始化数据库并启动服务器。

1. 双击 `start.bat`。
2. 脚本会自动检测 Node.js 和 npm 是否安装，若未安装会提示。
3. 如果 `node_modules` 缺失，会自动安装依赖。
4. 如果数据库文件不存在，会自动运行迁移。
5. 启动成功后，会自动打开默认浏览器访问 `http://localhost:3000`。
6. 如果端口 3000 已被占用，脚本会提示选择：
   - 打开浏览器访问已有服务器
   - 终止现有服务器并启动新实例
   - 退出

### 一键安装包（Windows）

对于没有 Node.js 环境的用户，我们提供了打包好的可执行文件。

1. 下载 `finance-manager.exe`（位于 `dist/` 目录）。
2. 双击运行，自动启动服务器并打开浏览器。
3. 关闭窗口即可停止服务器。

> 注意：一键安装包已内置 Node.js 运行时，无需额外安装。

## 项目结构

```
finance-management-system/
├── config/           # 配置文件（数据库、环境变量）
├── src/              # 后端源代码
│   ├── models/       # 数据模型
│   ├── repositories/ # 仓库层（数据访问抽象）
│   ├── services/     # 业务逻辑层
│   ├── routes/       # API 路由
│   ├── middleware/   # 中间件（认证、验证）
│   └── utils/        # 工具函数
├── public/           # 前端静态文件
│   ├── index.html    # 主页面
│   ├── css/          # 样式表
│   ├── js/           # JavaScript 模块
│   └── assets/       # 图片等资源
├── database/         # 数据库相关
│   ├── migrations/   # 迁移脚本
│   └── finance.db    # SQLite 数据库文件（自动生成）
├── scripts/          # 辅助脚本（打包脚本等）
├── plans/            # 设计文档和架构图
├── server.js         # 主服务器文件
├── start.bat         # Windows 一键启动脚本
├── package.json      # 项目配置
└── README.md         # 本文档
```

## API 文档

### 认证

- `POST /api/auth/register` - 注册新用户
- `POST /api/auth/login` - 登录，获取 JWT
- `POST /api/auth/logout` - 注销（客户端清除 token）

### 用户管理

- `GET /api/users/me` - 获取当前用户信息
- `PUT /api/users/me` - 更新用户信息

### 分类管理

- `GET /api/categories` - 获取分类列表
- `POST /api/categories` - 创建分类
- `PUT /api/categories/:id` - 更新分类
- `DELETE /api/categories/:id` - 删除分类

### 交易管理

- `GET /api/transactions` - 获取交易列表（支持分页、过滤）
- `POST /api/transactions` - 创建交易
- `PUT /api/transactions/:id` - 更新交易
- `DELETE /api/transactions/:id` - 删除交易
- `GET /api/transactions/export?format=csv` - 导出交易数据（CSV/Excel）

### 数据分析

- `GET /api/analytics/monthly?year=2025` - 获取月度收入支出统计
- `GET /api/analytics/category?type=expense` - 获取分类占比
- `GET /api/analytics/trend?months=6` - 获取趋势图表数据

详细 API 说明参考 [API 设计](plans/architecture.md#5-api-接口设计)。

## 开发指南

### 代码规范

- 使用 JavaScript ES6+ 语法。
- 所有函数、类、模块需添加 JSDoc 注释。
- 遵循 Airbnb JavaScript 风格指南。

### 新增功能步骤

1. 在 `src/models/` 中定义数据模型（如需新表）。
2. 在 `src/repositories/` 中实现仓库类。
3. 在 `src/services/` 中编写业务逻辑。
4. 在 `src/routes/` 中创建路由。
5. 在 `public/js/` 中编写前端逻辑。

### 测试

运行单元测试：
```bash
npm test
```

### 生成可执行文件

```bash
npm run build
```

生成的可执行文件位于 `dist/finance-manager.exe`。

## 部署

### 本地部署

参考"快速开始"部分。

### 生产部署建议

1. 将数据库切换为 PostgreSQL，修改 `config/database.js`。
2. 使用 PM2 或 Docker 运行。
3. 配置 Nginx 反向代理。

## 故障排除

### 1. 无法启动服务器，端口被占用

- 修改 `.env` 中的 `PORT` 变量。
- 或使用 `start.bat` 脚本，它会自动检测并提示解决方案。

### 2. 数据库迁移失败

- 确保 `database/` 目录有写权限。
- 检查是否已安装 Visual Studio 构建工具（Windows）。

### 3. 前端页面无法加载

- 检查 `public/index.html` 是否存在。
- 确保服务器正确配置了静态文件服务。

### 4. 一键安装包无法运行

- 可能是防病毒软件拦截，请添加例外。
- 确保系统为 Windows 10/11 64 位。

### 5. 启动脚本（start.bat）窗口快速关闭

- 旧版本脚本在遇到错误时会直接退出。新版已增加错误暂停。
- 如果仍快速关闭，请手动打开命令行，进入项目目录执行 `npm start` 查看具体错误。

## 优雅关闭与数据保存

服务器支持多种优雅关闭方式，确保数据持久化和用户友好的关闭体验：

### 1. 前端关闭服务器功能
- **位置**：登录后，点击右上角用户名下拉菜单中的"关闭服务器"选项。
- **功能**：显示确认对话框和进度指示器，发送关闭请求到服务器。
- **流程**：
  1. 用户点击"关闭服务器"
  2. 显示确认对话框
  3. 显示进度模态框（包含进度条和状态消息）
  4. 发送带JWT认证的POST请求到 `/api/shutdown`
  5. 服务器接收请求后保存数据库并关闭进程
  6. 前端显示"服务器已成功关闭"的最终状态
  7. 提供"尝试重新连接"、"关闭浏览器标签页"、"继续查看当前页面"等选项

### 2. 命令行关闭
- 按下 **Ctrl+C** 或在命令行发送 SIGINT 信号，服务器会先保存数据库再退出。
- 程序收到 SIGTERM 信号时也会执行优雅关闭。

### 3. API 关闭接口
- `POST /api/shutdown` - 安全关闭服务器端点
  - **认证**：需要有效的 JWT Token（Bearer Token）
  - **权限**：任何登录用户均可调用
  - **响应**：`{"message": "关机命令已接收", "userId": 1, "username": "test0", "timestamp": "..."}`
  - **服务器行为**：保存数据库，延迟500毫秒后关闭HTTP服务器并退出进程

### 4. 自动保存机制
- 服务器每30秒自动保存数据库一次，防止数据丢失。
- 在关闭前会强制执行一次完整保存。

### 5. 故障恢复
- 如果服务器意外关闭，重启时会自动加载最近保存的数据库文件。
- 前端检测到关闭请求失败或网络错误时，会显示友好的错误信息和重试选项。

### 技术实现细节
- **前端**：`public/js/app.js` 中的 `shutdownServer()` 函数
- **后端**：`server.js` 中的 `/api/shutdown` 路由，使用 JWT 认证中间件
- **安全**：已移除仅限本地IP的限制，改为使用JWT认证，使局域网内其他设备也能安全关闭服务器

## 贡献

欢迎提交 Issue 或 Pull Request。

## 免责声明（内测版本）

**重要提醒**：此版本为内部测试版本（V0.1），可能存在未发现的错误、数据丢失风险或功能不完整的情况。开发者不对使用本软件造成的任何数据损失或系统问题承担责任。

**测试建议**：
1. 请勿在生产环境中使用本系统
2. 建议在虚拟机或测试环境中运行
3. 定期备份数据库文件（`database/finance.db`）
4. 如发现问题，请在GitHub Issues中反馈

## 许可证

MIT