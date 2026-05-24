# Git 使用指南

## 基础操作
1. `git add` —— 将文件添加到暂存区。
2. `git commit` —— 将暂存区内容提交到版本库。
3. `git checkout` —— 用版本库里的版本替换工作区的版本。
4. `git rm` —— 删除文件。注意：从未被添加到版本库就被删除的文件无法恢复。
5. `git status` —— 查看当前仓库状态。
6. `git reset --hard/soft` —— 版本回退。
7. `git reflog` —— 查看所有操作记录（包括回退前的提交）。
8. `git log` —— 查看历史记录。  
   - `--graph`：显示分支合并图  
   - `--pretty=oneline`：简化输出（每行一个提交）
9. `cat <文件>` —— 查看文件内容（工作区）。

## 远程仓库操作
10. `git push` —— 将本地库的内容推送到远程仓库。  
    - `-u` 参数（首次推送）：`git push -u origin main`  
    - 后续推送：`git push origin main`
11. `git remote` —— 管理远程仓库绑定。  
    - `git remote rm <name>`：解除本地和远程的绑定  
    - `git remote add origin git@server-name:path/repo-name.git`：关联一个远程库（`origin` 是默认远程库命名）
12. `git clone` —— 从远程克隆仓库到本地（推荐使用 SSH 协议）。
13. `git remote -v` —— 查看远程库详细信息。
14. `git push origin master/dev` —— 将主分支或开发分支上的本地提交推送到远程仓库。

## 分支管理
- **主分支**：`main`（或 `master`），HEAD 指向当前分支，分支指针指向提交。
- **常用操作**：
  1. 创建并切换到新分支：  
     `git checkout -b dev` 或 `git switch -c dev`
  2. 直接切换分支：  
     `git switch main`
  3. 查看所有分支：  
     `git branch`
  4. 创建分支：  
     `git branch <分支名>`
  5. 合并分支：  
     - 先切换到目标分支（如 `main`），再执行 `git merge dev`  
     - 合并后可删除 `dev` 指针：`git branch -d dev`
  6. 合并分支冲突：手动修改冲突文件，然后 `add`、`commit`。
  7. 禁用 Fast‑Forward 合并（保留分支历史）：  
     `git merge --no-ff -m "merge with no-ff" dev`  
     （该命令会生成一个新的合并提交）
  8. 强制删除未合并的分支：  
     `git branch -D <分支名>`

## 临时储存与修复
- **`git stash`** —— 储藏当前工作现场（例如临时修复 bug）。
  - `git stash apply`：恢复工作区（stash 内容仍保留）
  - `git stash drop`：删除 stash 内容
  - `git stash pop`：恢复并删除 stash 内容
  - `git stash list`：查看所有 stash 记录
- **`git cherry-pick <提交编号>`** —— 将特定提交复制到当前分支。

## 多人协作要点
1. 在另一台电脑（或另一个目录）中 `git clone` 仓库，默认只看到 `main` 分支。
2. 创建并切换到本地 `dev` 分支，并关联远程的 `origin/dev`：  
   `git checkout -b dev origin/dev`
3. 在 `dev` 上开发，推送时使用 `git push origin dev`。
4. 推送发生冲突时，先用 `git pull` 抓取最新提交，在本地解决冲突，再推送。

## 注意事项
- 合并分支前确保工作区是干净的（已 `add` 并 `commit` 或 `stash`）。
- 删除未跟踪的文件无法恢复，使用 `rm` 或 `git clean` 时要小心。
- `git reset --hard` 会丢弃所有未提交的修改，慎用。