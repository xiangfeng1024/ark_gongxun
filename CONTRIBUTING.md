# 贡献指南

欢迎提交问题反馈、文档改进和代码贡献。

本仓库只维护 `main` 一个分支。所有 PR 都提交到 `main`，其他人在自己的 Fork 中完成修改。

## 从克隆到提交 PR（PowerShell 7）

前提：已经安装 Git，有 GitHub 账号，并能向自己的仓库推送。

1. 打开 https://github.com/xiangfeng1024/ark_gongxun/fork ，Fork 到自己的账号，保留仓库名，选择只复制 `main`。
2. 在准备保存项目的父目录执行以下命令，将用户名替换为自己的 GitHub 用户名：

```powershell
$githubUser = 'YOUR_GITHUB_USERNAME'
git clone "https://github.com/$githubUser/ark_gongxun.git"
cd ark_gongxun
git remote add upstream https://github.com/xiangfeng1024/ark_gongxun.git
git switch main
git fetch upstream
git merge --ff-only upstream/main
git push origin main
```

`origin` 是自己的 Fork，`upstream` 是原仓库。以下示例也只使用 Fork 的 `main`，一次处理一个 PR；未合并前继续推送会更新同一个 PR。

3. 以修改 README 为例，保存文件后检查、提交并推送：

```powershell
notepad README.md
# 保存并关闭编辑器后执行
git diff --check
git diff
git add README.md
git commit -m "docs: 完善项目说明"
git push origin main
```

如果 Git 提示没有作者信息，先在本仓库配置自己的姓名和提交邮箱，再重新提交：

```powershell
git config user.name '你的名字'
git config user.email '你的 GitHub 提交邮箱'
```

4. 在同一个 PowerShell 会话中打开 PR 比较页面：

```powershell
Start-Process "https://github.com/xiangfeng1024/ark_gongxun/compare/main...${githubUser}:ark_gongxun:main?expand=1"
```

确认目标是 `xiangfeng1024/ark_gongxun:main`，来源是自己 Fork 的 `main`。点击 **Create pull request**，填写修改目的、内容和验证方式，提交后等待维护者审查。打开页面本身不会自动创建 PR。

如需补充修改，继续编辑、提交并执行 `git push origin main`，已有 PR 会自动更新。

5. PR 合并后，本地没有未提交修改时，同步上游再开始下次修改：

```powershell
git fetch upstream
git merge --ff-only upstream/main
git push origin main
```

如果 `--ff-only` 报错，说明历史已经分叉（例如 PR 通过 Squash 或 Rebase 合并），请先处理已有提交；不要直接强制覆盖。维护者使用普通 Merge 合并时，可直接按以上流程继续。

参考：[GitHub 官方说明：从 Fork 创建 PR](https://docs.github.com/en/pull-requests/how-tos/create-pull-requests/creating-a-pull-request-from-a-fork)。

所有人均可提交 PR，但只有仓库所有者 @xiangfeng1024 有权合并。主分支受到规则保护，不向外部贡献者授予写入或管理权限。

提交内容前，请确认你有权以本仓库的 MIT 许可证贡献这些内容，且不包含密码、访问令牌、个人隐私或未经授权的第三方材料。
