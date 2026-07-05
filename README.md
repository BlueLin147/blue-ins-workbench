# Blue's INS Workbench — Render 上线部署指南

本项目是 **Blue's INS Workbench**（Instagram 客户线索/人员数据过滤导出工作台）的 Render 静态上线部署包。
已优化本地依赖，将 SheetJS (`xlsx.full.min.js`) 改为本地托管，避免国内或特殊网络下第三方 CDN 跨域或加载慢的问题，实现极速响应、零插件直开。

---

## 🚀 如何部署上线到 Render (完全免费，永久不休眠！)

Render 的 **Static Site（静态站点）** 服务完全免费，配备全球高速 CDN，且**不会像 Web Services 那样 15 分钟无操作自动休眠**，非常适合作业工作台上线。

### 第一步：推送到 GitHub 仓库

1. 在 GitHub 上新建一个空仓库（例如命名为 `blue-ins-workbench`）。
2. 打开终端，进入本项目目录并提交推送：

```bash
cd /Users/blue/.gemini/antigravity/scratch/blue-ins-workbench-deploy

# 初始化 Git 仓库
git init
git add .
git commit -m "feat: Blue's INS Workbench ready for Render static deploy"

# 绑定远程仓库并推送（请将其中的 <你的GitHub用户名> 替换为你自己的用户名）
git remote add origin https://github.com/<你的GitHub用户名>/blue-ins-workbench.git
git branch -M main
git push -u origin main
```

---

### 第二步：在 Render 控制台一键上线

部署有以下两种方式，任选其一即可：

#### 方案 A（推荐：使用 Blueprint 一键部署）
1. 登录 [Render 控制台 (Dashboard)](https://dashboard.render.com/)。
2. 点击右上角的 **New +** 按钮 -> 选择 **Blueprint**。
3. 在列表中找到并勾选你刚刚推送的 `blue-ins-workbench` 仓库 -> 点击 **Connect**。
4. Render 会自动识别项目中的 `render.yaml` 配置文件，点击 **Apply**。
5. 等待几十秒，部署成功！你将获得一个永久免费的 HTTPS 公网域名（例如 `https://blue-ins-workbench.onrender.com`）。

#### 方案 B（手动创建 Static Site）
1. 在 Render 控制台点击 **New +** -> 选择 **Static Site**。
2. 关联并勾选你的 `blue-ins-workbench` 仓库。
3. 填写部署配置：
   - **Name**: `blue-ins-workbench`（可自定义，决定了二级域名的前缀）
   - **Branch**: `main`
   - **Build Command**: `echo no build needed`（或留空）
   - **Publish Directory**: `.`（代表当前根目录）
4. 点击 **Create Static Site**，等待构建上线即可。

---

## 💡 日后修改与维护

以后如果需要修改工作台页面样式或逻辑：
1. 直接修改本目录下的 `index.html`。
2. 执行 `git add . && git commit -m "update" && git push`。
3. Render 检测到 GitHub 代码仓库更新后，会自动触发重部署（约十几秒即可同步到线上）。
