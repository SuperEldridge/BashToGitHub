# Git 完整命令教程

从新建项目到分支合并的全流程命令参考

---

## 📋 目录

- [初始设置](#初始设置)
- [创建新项目](#创建新项目)
- [分支管理](#分支管理)
- [提交和推送](#提交和推送)
- [代码审查](#代码审查)
- [分支合并](#分支合并)
- [常用命令速查](#常用命令速查)

---

## 🎯 初始设置

### 配置Git

```bash
# 设置用户名
git config --global user.name "你的用户名"

# 设置邮箱
git config --global user.email "你的邮箱"

# 查看所有配置
git config --list
```

### 生成SSH密钥

```bash
# 生成SSH密钥对
ssh-keygen -t ed25519 -C "your_email@example.com" -f ~/.ssh/id_ed25519 -N ""

# 复制公钥到剪贴板
cat ~/.ssh/id_ed25519.pub | clip

# 测试连接到GitHub
ssh -T git@github.com
```

**注意：** 需要在GitHub上添加SSH密钥：Settings → SSH and GPG keys → New SSH key

---

## 📁 创建新项目

### 初始化仓库

```bash
# 进入项目目录
cd "C:\Users\Eldridge\Desktop\your-project"

# 初始化Git仓库
git init

# 查看当前状态
git status
```

### 首次提交和推送

```bash
# 添加所有文件到暂存区
git add .

# 提交代码
git commit -m "初始提交"

# 关联远程仓库
git remote add origin git@github.com:用户名/仓库名.git

# 查看远程仓库
git remote -v

# 推送到GitHub（首次推送）
git push -u origin master
```

---

## 🌿 分支管理

### 查看分支

```bash
# 查看所有本地分支
git branch

# 查看所有分支（包括远程）
git branch -a

# 查看分支详情（包含最新提交）
git branch -v
```

### 创建和切换分支

```bash
# 创建新分支
git branch feature-新功能

# 创建并切换到新分支
git checkout -b feature-新功能

# 切换到已有分支
git checkout master

# 切换到上一个分支
git checkout -
```

### 删除分支

```bash
# 删除本地分支（已合并）
git branch -d feature-新功能

# 强制删除分支（未合并）
git branch -D feature-新功能

# 删除远程分支
git push origin --delete feature-新功能
```

---

## 💾 提交和推送

### 本地提交

```bash
# 查看当前状态
git status

# 查看未暂存的修改
git diff

# 查看已暂存的修改
git diff --staged

# 添加特定文件
git add 文件名

# 添加所有文件
git add .

# 添加所有修改（包括删除）
git add -A

# 提交代码
git commit -m "提交信息"

# 修改上一次提交
git commit --amend
```

### 推送到GitHub

```bash
# 推送当前分支
git push

# 首次推送并设置上游分支
git push -u origin feature-新功能

# 推送所有分支
git push --all

# 推送标签
git push --tags
```

### 从GitHub拉取

```bash
# 拉取并合并
git pull

# 拉取但不合并
git fetch

# 拉取特定分支
git pull origin feature-新功能
```

---

## 🔍 代码审查

### 在VS Code中审查

```bash
# 用VS Code打开项目
code -r .

# 在VS Code中：
# - 左下角分支图标 → 点击 → 选择分支
# - 源代码管理 → 查看提交历史和变更
# - 右键文件 → "打开更改" → 对比视图
```

### 使用命令行审查

```bash
# 切换到要审查的分支
git checkout feature-display-time

# 查看文件内容
cat 3d-shapes.html

# 查看与master的差异
git diff master

# 查看差异统计
git diff --stat

# 查看提交历史
git log --oneline

# 查看分支图形
git log --graph --oneline --all
```

### 导出文件对比

```bash
# 保存不同分支的文件
git checkout feature-display-time
cp 3d-shapes.html clock.html

git checkout feature-orchestra
cp 3d-shapes.html orchestra.html

# 在VS Code中对比
code -d clock.html orchestra.html
```

---

## 🔄 分支合并

### 方法A：GitHub Pull Request（推荐）

1. 打开GitHub仓库页面
2. 点击 "Pull requests" 标签
3. 点击 "New pull request"
4. 选择要合并的分支：
   - base: `master`（目标分支）
   - compare: `feature-新功能`（源分支）
5. 查看代码差异
6. 填写标题和描述
7. 点击 "Create pull request"
8. 点击 "Merge pull request"
9. 点击 "Confirm merge"
10. （可选）删除已合并的分支

### 方法B：命令行合并（快速）

```bash
# 切换到master分支
git checkout master

# 拉取最新代码
git pull

# 合并功能分支
git merge feature-新功能

# 推送到GitHub
git push

# 删除已合并的本地分支
git branch -d feature-新功能

# 删除远程分支
git push origin --delete feature-新功能
```

### 合并两个功能分支

```bash
# 先合并两个功能分支
git checkout feature-分支1
git merge feature-分支2
git push

# 然后合并到master
git checkout master
git merge feature-分支1
git push

# 清理分支
git branch -d feature-分支2
git push origin --delete feature-分支2
```

---

## ⚡ 常用命令速查

| 操作 | 命令 |
|---|---|
| **配置** | `git config --global user.name/email` |
| **初始化** | `git init` |
| **克隆** | `git clone <url>` |
| **查看状态** | `git status` |
| **添加文件** | `git add .` 或 `git add <file>` |
| **提交** | `git commit -m "信息"` |
| **查看差异** | `git diff` |
| **查看分支** | `git branch` 或 `git branch -v` |
| **创建分支** | `git checkout -b <分支名>` |
| **切换分支** | `git checkout <分支名>` |
| **合并分支** | `git merge <分支名>` |
| **删除分支** | `git branch -d <分支名>` |
| **推送** | `git push` 或 `git push -u origin <分支>` |
| **拉取** | `git pull` |
| **查看历史** | `git log --oneline` |
| **关联远程** | `git remote add origin <url>` |
| **查看远程** | `git remote -v` |

---

## 💡 工作流程总结

### 日常开发（单个分支）

```bash
git add .                              # 添加修改
git commit -m "描述"                    # 提交
git push                                # 推送
```

### 功能开发（分支工作流）

```bash
# 创建功能分支
git checkout -b feature-新功能

# 开发并提交
git add .
git commit -m "实现新功能"

# 推送到远程
git push -u origin feature-新功能

# 审查通过后合并
git checkout master
git merge feature-新功能
git push

# 清理分支
git branch -d feature-新功能
```

### 只在本地保存（不推送）

```bash
git add .
git commit -m "本地保存"
# 不运行 git push
```

---

## 🎨 VS Code 快捷操作

| 操作 | 快捷键 |
|---|---|
| 打开命令面板 | `Ctrl+Shift+P` |
| 切换分支 | 点击左下角分支图标 |
| 查看更改 | `Ctrl+Shift+G` |
| 对比文件 | 右键文件 → "打开更改" |
| 提交更改 | 源代码管理面板 → 勾选 → 填写信息 → 提交 |

---

## ❓ 常见问题

### Q: 在时钟分支中 push 到哪里？
A: 推送到当前所在的分支（feature-display-time），不是master

### Q: 不想 push 时怎么保存？
A: 只需要 `git add` 和 `git commit`，不运行 `git push`

### Q: 如何查看两个分支的差异？
A: `git diff 分支1 分支2`

### Q: 合并时出现冲突怎么办？
A: 编辑冲突文件 → `git add` → `git commit` → `git push`

---

*创建日期：2026-03-05*
