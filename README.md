# BookUniverse

基于 Cloudflare Pages + React + Vite 构建的在线图书管理系统。

## 技术栈

- **前端**: React 19 + TypeScript + Vite
- **后端**: Cloudflare Pages Functions (TypeScript)
- **数据库**: Cloudflare D1 (SQLite)
- **存储**: Cloudflare R2
- **部署**: Cloudflare Pages

## 开发

```bash
# 安装依赖
npm install

# 本地开发
npm run dev

# 构建
npm run build

# 本地预览（带 Functions）
npm run pages:dev
```

## 数据库

```bash
# 创建 D1 数据库
npm run db:create

# 运行迁移（本地）
npm run db:migrate:local

# 运行迁移（生产）
npm run db:migrate:remote
```

## 部署

项目通过 Cloudflare Pages 自动部署，连接 GitHub 仓库后每次推送到 main 分支会自动构建和部署。

手动部署：
```bash
npm run pages:deploy
```
