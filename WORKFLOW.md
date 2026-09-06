# BookUniverse 开发工作流

## 项目信息

- **仓库**: https://github.com/Restone0616/BookUniverse
- **D1 数据库**: bookuniverse-db (a2ab4528-ced2-44d6-9c82-ec900a798fdd)
- **R2 存储桶**: library
- **主分支**: main

## 开发流程

### 1. 日常开发

对于小改动，可以直接在本地修改并测试：

```bash
# 启动本地开发服务器
npm run dev

# 访问 http://localhost:5173
```

### 2. 较大改动（推荐）

当改动较大或需要测试 Cloudflare Functions 时：

```bash
# 1. 创建新分支
git checkout -b feature/your-feature-name

# 2. 进行开发工作
# ... 编辑代码 ...

# 3. 提交更改
git add .
git commit -m "描述你的改动"

# 4. 推送分支到 GitHub
git push -u origin feature/your-feature-name

# 5. 构建项目
npm run build

# 6. 部署到预览环境（分支部署）
npx wrangler pages deploy dist --project-name bookuniverse --branch feature/your-feature-name

# 7. 获取预览 URL 并测试
# Wrangler 会输出预览地址，格式类似：
# https://feature-your-feature-name.bookuniverse.pages.dev
```

### 3. 合并到生产环境

经过测试确认无误后：

```bash
# 1. 切换回主分支
git checkout main

# 2. 合并功能分支
git merge feature/your-feature-name

# 3. 推送到 GitHub（触发自动部署）
git push

# 或者手动部署
npm run pages:deploy
```

## 数据库操作

### 本地数据库

```bash
# 应用迁移
npm run db:migrate:local

# 查询数据
npx wrangler d1 execute bookuniverse-db --local --command "SELECT * FROM books"
```

### 生产数据库

```bash
# 应用迁移
npm run db:migrate:remote

# 查询数据（谨慎操作）
npx wrangler d1 execute bookuniverse-db --remote --command "SELECT * FROM books"
```

## Cloudflare Pages 连接

1. 登录 Cloudflare Dashboard
2. 进入 Pages 页面
3. 点击 "Create application" → "Connect to Git"
4. 选择 GitHub 账号并授权
5. 选择 `Restone0616/BookUniverse` 仓库
6. 配置构建设置：
   - **Framework preset**: Vite
   - **Build command**: `npm run build`
   - **Build output directory**: `dist`
7. 添加环境变量（如需要）
8. 点击 "Save and Deploy"

之后每次推送到 main 分支都会自动构建和部署。

## 注意事项

- ✅ 较大改动请创建分支工作
- ✅ 使用 wrangler 部署预览测试
- ✅ 测试通过后再合并到 main
- ❌ 不要使用 `npm run dev` 测试 Functions（无法运行 Cloudflare Functions）
- ❌ 生产数据库操作需谨慎
