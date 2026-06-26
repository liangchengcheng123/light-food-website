# {{研究项目名称}} 研究网站

这是一个用于微博开放平台网站应用申请和 OAuth 回调配置的静态个人研究网站。

网站用途：

- 展示研究者身份；
- 展示“青年轻食行为与当代青年生活方式”研究项目；
- 说明数据来源、隐私保护和研究伦理；
- 作为微博开放平台 API 申请中的“应用网址”；
- 作为 OAuth Redirect URI 的 `callback.html` 承载页面。

## 项目结构

```text
research-oauth-site/
├── index.html
├── research.html
├── privacy.html
├── callback.html
├── contact.html
├── style.css
├── README.md
└── assets/
    └── research-visual.svg
```

## 本地预览

方式一：直接双击 `index.html` 打开。

方式二：使用本地静态服务预览：

```bash
python3 -m http.server 8000
```

然后访问：

```text
http://localhost:8000
```

## 部署到 GitHub Pages

1. 新建一个 GitHub 仓库，例如 `light-food-research-site`。
2. 将本项目文件上传到仓库根目录。
3. 进入仓库 `Settings`。
4. 进入 `Pages`。
5. Source 选择 `Deploy from a branch`。
6. Branch 选择 `main`，目录选择 `/root`。
7. 保存后等待部署完成。

部署完成后，网站通常类似：

```text
https://你的GitHub用户名.github.io/light-food-research-site/
```

## 部署到 Vercel

1. 登录 Vercel。
2. 选择 `Add New Project`。
3. 导入存放本项目的 GitHub 仓库。
4. Framework Preset 选择 `Other` 或保持默认静态站点设置。
5. 不需要设置数据库或服务端环境变量。
6. 点击 Deploy。

部署完成后，网站通常类似：

```text
https://你的项目名.vercel.app/
```

## 部署到 Netlify

1. 登录 Netlify。
2. 选择 `Add new site`。
3. 可以选择从 GitHub 导入项目，也可以直接拖拽本项目文件夹上传。
4. Build command 留空。
5. Publish directory 如果项目在仓库根目录，则填写 `.`。
6. 点击 Deploy。

部署完成后，网站通常类似：

```text
https://你的项目名.netlify.app/
```

## 微博开放平台“应用网址”填写

应用网址建议填写网站首页地址：

```text
{{网站域名}}/index.html
```

如果部署平台默认首页可直接访问，也可以填写：

```text
{{网站域名}}/
```

示例：

```text
https://你的GitHub用户名.github.io/light-food-research-site/
```

## OAuth Redirect URI 填写

OAuth Redirect URI 应填写 `callback.html` 的完整线上地址：

```text
{{网站域名}}/callback.html
```

示例：

```text
https://你的GitHub用户名.github.io/light-food-research-site/callback.html
```

当微博 OAuth 授权成功后，平台会将授权码追加到回调地址，例如：

```text
https://你的GitHub用户名.github.io/light-food-research-site/callback.html?code=授权码
```

`callback.html` 会读取 URL 参数中的 `code` 并显示在页面上。请复制该授权码，并在本地后端脚本中换取 `access_token`。

## 为什么不能把 App Secret 写在前端代码中

前端 HTML、CSS、JavaScript 会被浏览器完整下载，任何访问网站的人都可以查看源代码。如果把 `App Secret`、`Access Token` 或其他密钥写在前端代码中，就等于公开泄露密钥。

正确做法：

- 前端页面只接收并显示 OAuth 返回的 `code`；
- 使用本地后端脚本或安全服务端环境请求 access token；
- `App Secret` 只保存在本地环境变量、服务器环境变量或安全密钥管理系统中；
- 不在 GitHub、网页源码、浏览器 LocalStorage 或公开日志中保存密钥。

## 占位符替换

部署前请替换以下占位符：

```text
{{姓名}}
{{学校}}
{{学院}}
{{邮箱}}
{{研究项目名称}}
{{网站域名}}
```

建议将 `{{网站域名}}` 替换为最终部署后的完整域名，例如：

```text
https://你的GitHub用户名.github.io/light-food-research-site
```

