# MSML 2027 网站：保存修改并生成链接 / 本地分享

按下面步骤在**本机终端**（Cursor 终端或 PowerShell）中操作。所有命令都在项目目录 `c:\Users\MYW\Desktop\Todo\jekyll\jekyll` 下执行。

---

## 不发布到 GitHub 时，怎么分享给别人看？

### 方式一：同一 WiFi / 局域网内分享（最省事）

别人和你连的是**同一个 WiFi 或同一局域网**时：

1. 在项目目录启动 Jekyll，并允许本机被访问：
   ```powershell
   cd c:\Users\MYW\Desktop\Todo\jekyll\jekyll
   bundle exec jekyll serve --host 0.0.0.0
   ```
2. 查看本机 IP：在终端执行 `ipconfig`，找到 **IPv4 地址**（如 `192.168.1.105`）。
3. 把链接发给对方：**http://你的IP:4000**（例如 `http://192.168.1.105:4000`）。
4. 对方在浏览器打开该链接即可查看。你的电脑和 Jekyll 终端需要一直开着。

---

### 方式二：打包发给对方，对方本地打开

1. 在项目目录生成网站：
   ```powershell
   cd c:\Users\MYW\Desktop\Todo\jekyll\jekyll
   bundle exec jekyll build
   ```
2. 将整个 **`_site`** 文件夹打成 zip，通过 U 盘、网盘或邮件发给对方。
3. 对方解压后：
   - **直接双击 `_site/index.html`** 可以看首页，但部分链接可能异常（因为是 file:// 打开）。
   - **更稳妥**：在解压后的 `_site` 文件夹里打开终端，执行  
     `python -m http.server 8080`（需已装 Python），然后浏览器打开 **http://localhost:8080** 查看。

---

### 方式三：临时公网链接（对方不在同一 WiFi 也能看）

用 **ngrok** 或 **localtunnel** 把本机的 4000 端口暴露成一个临时网址，任何人点链接即可查看（无需 GitHub）。

**用 ngrok 示例：**

1. 到 https://ngrok.com 注册并下载 ngrok，解压。
2. 先在本机启动网站：
   ```powershell
   bundle exec jekyll serve
   ```
3. 在**另一个终端**运行（把 ngrok 放在 PATH 或写全路径）：
   ```powershell
   ngrok http 4000
   ```
4. 终端里会显示类似 `https://xxxx.ngrok.io` 的地址，把该地址发给对方即可。关闭 ngrok 或关机后，该链接会失效。

---

## 发布到 GitHub Pages（生成长期链接）

---

## 一、安装 Git（若尚未安装）

1. 打开 https://git-scm.com/download/win 下载 Windows 版 Git。
2. 安装时勾选 **“Add Git to PATH”**。
3. 安装完成后**关闭并重新打开**终端。

在终端输入 `git --version`，能显示版本号即表示安装成功。

---

## 二、保存当前所有修改（提交到 Git）

在终端中依次执行：

```powershell
# 1. 进入项目目录
cd c:\Users\MYW\Desktop\Todo\jekyll\jekyll

# 2. 若从未初始化过 Git，先执行（若已有 .git 可跳过）
git init

# 3. 添加所有文件
git add .

# 4. 提交并写一条说明
git commit -m "MSML 2027 site: save current changes"
```

若提示 “nothing to commit” 或 “no changes”，说明当前修改已经提交过，可直接进行下一步。

---

## 三、在 GitHub 上创建仓库

1. 登录 https://github.com 。
2. 点击右上角 **“+”** → **“New repository”**。
3. 填写：
   - **Repository name**：例如 `msml2027`（或 `你的用户名.github.io` 若希望链接为 `https://用户名.github.io/`）。
   - **Public**。
   - **不要**勾选 “Add a README file” 等（保持空仓库）。
4. 点击 **“Create repository”**。

创建后页面会显示仓库地址，形如：`https://github.com/你的用户名/msml2027.git`。

---

## 四、把本地项目推送到 GitHub

在**同一终端、同一项目目录**下执行（把下面两处的 `你的用户名` 和 `msml2027` 换成你自己的）：

```powershell
# 添加远程仓库（替换为你的仓库地址）
git remote add origin https://github.com/你的用户名/msml2027.git

# 主分支命名为 main（若已存在可忽略）
git branch -M main

# 推送到 GitHub（会提示登录或弹窗认证）
git push -u origin main
```

- 若之前已经添加过 `origin`，可先执行：`git remote remove origin`，再执行上面的 `git remote add origin ...`。
- 若推送时要求登录，按提示在浏览器中完成 GitHub 登录或使用 Personal Access Token。

---

## 五、开启 GitHub Pages 并生成链接

1. 在浏览器打开你的仓库页面：`https://github.com/你的用户名/msml2027`。
2. 点击 **Settings**（设置）。
3. 左侧找到 **Pages**。
4. 在 **Build and deployment** 下：
   - **Source** 选 **Deploy from a branch**。
   - **Branch** 选 **main**，文件夹选 **/ (root)**。
   - 点击 **Save**。
5. 等待约 1～2 分钟，同一页面会显示绿色提示和你的站点地址。

**若仓库名是 `msml2027`**，链接一般为：

**https://你的用户名.github.io/msml2027/**

---

## 六、若使用项目仓库（如 msml2027），需设置 baseurl

否则页面样式和跳转可能错乱。

1. 用编辑器打开项目里的 `_config.yml`。
2. 找到 `baseurl:`，改成你的仓库名（注意前面有斜杠）：

   ```yaml
   baseurl: "/msml2027"
   ```

3. 保存后再次提交并推送：

   ```powershell
   git add _config.yml
   git commit -m "Set baseurl for GitHub Pages"
   git push
   ```

4. 再等 1～2 分钟，用 **https://你的用户名.github.io/msml2027/** 打开，检查样式和链接是否正常。

---

## 七、之后如何更新网站

每次改完本地文件后，在项目目录执行：

```powershell
git add .
git commit -m "更新说明（随便写一句）"
git push
```

推送后 GitHub 会自动重新构建，约 1～2 分钟后刷新你的 Pages 链接即可看到更新。

---

## 常见问题

| 情况 | 处理 |
|------|------|
| `git` 不是内部或外部命令 | 安装 Git 并确保勾选 “Add to PATH”，重启终端。 |
| 推送时要求登录 | 在浏览器完成登录，或使用 GitHub Personal Access Token 作为密码。 |
| 页面 404 | 确认 Settings → Pages 里 Branch 选的是 main、目录为 / (root)，并等待 1～2 分钟。 |
| 样式错乱、链接点不对 | 若仓库名不是 `用户名.github.io`，必须在 `_config.yml` 里设置 `baseurl: "/仓库名"` 并重新推送。 |

完成以上步骤后，你的站点就会有一个类似 **https://你的用户名.github.io/msml2027/** 的固定链接。
