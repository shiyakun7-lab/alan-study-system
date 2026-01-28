# GitHub Pages 部署指南

## 前提条件
- 已有GitHub账号（如果没有，请访问 https://github.com 注册）
- 本地代码已提交到Git仓库

## 部署步骤

### 1. 在GitHub上创建新仓库

1. 访问 https://github.com/new
2. 仓库名称填写：`alan-study-system`
3. 描述（可选）：Alan的自驱进化计划 - 小学生学习管理系统
4. 选择 **Public**（公开仓库，才能使用免费的GitHub Pages）
5. **不要**勾选 "Initialize this repository with a README"
6. 点击 "Create repository"

### 2. 推送本地代码到GitHub

在终端中，进入项目目录并执行以下命令：

```bash
cd /Users/myfishly/alan-study-system

# 添加远程仓库（将 YOUR_USERNAME 替换为你的GitHub用户名）
git remote add origin https://github.com/YOUR_USERNAME/alan-study-system.git

# 推送代码到GitHub
git branch -M main
git push -u origin main
```

### 3. 启用GitHub Pages

1. 在GitHub仓库页面，点击 **Settings**（设置）
2. 在左侧菜单找到 **Pages**
3. 在 "Source" 部分：
   - Branch: 选择 `main`
   - Folder: 选择 `/ (root)`
4. 点击 **Save**

### 4. 访问你的网站

等待1-2分钟后，你的网站将在以下地址可用：

```
https://YOUR_USERNAME.github.io/alan-study-system/
```

（将 YOUR_USERNAME 替换为你的GitHub用户名）

## 更新网站

以后如果要更新网站内容，只需：

```bash
cd /Users/myfishly/alan-study-system

# 修改文件后...
git add .
git commit -m "更新说明"
git push
```

等待几分钟，网站会自动更新。

## 常见问题

### Q: 推送时要求输入用户名和密码？
A: GitHub已不再支持密码认证，需要使用Personal Access Token：
1. 访问 https://github.com/settings/tokens
2. 点击 "Generate new token (classic)"
3. 勾选 `repo` 权限
4. 生成后复制token
5. 推送时用token代替密码

### Q: 网站显示404？
A:
- 确认GitHub Pages已启用
- 确认选择了正确的分支（main）
- 等待几分钟让GitHub处理
- 确认仓库是Public（公开）

### Q: 如何自定义域名？
A: 在GitHub Pages设置中可以添加自定义域名，需要配置DNS记录。

## 技术支持

如遇问题，可以：
- 查看GitHub Pages文档：https://docs.github.com/pages
- 检查仓库的Actions标签页查看部署状态
