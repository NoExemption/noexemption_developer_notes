# 🐙 Git & GitHub 实践指南

本手册按日常开发频率由高到低排序，涵盖了从入门到高阶的所有核心指令。

---

## 一、 🚀 初次上传新仓库 (建立连接)
1. **初始化**：`git init` (在当前文件夹内创建 Git 档案库)
2. **暂存**：`git add .` (将当前所有文件加入暂存区，准备提交)
3. **存档**：`git commit -m "Initial commit"` (记录项目当前版本的首个快照)
4. **关联**：`git remote add origin [URL]` (将本地仓库连接至远程 GitHub 仓库)
5. **拉取**：`git pull origin main --rebase` (强制合并云端已有文件，确保起点一致)
6. **推送**：`git push -u origin main` (上传代码并建立本地与云端分支的追踪关系)

---

## 二、 🔄 日常同步更新 (最常用)
1. **拉取**：`git pull --rebase` (先拉取云端改动并让本地改动接在后面，保持线性历史)
2. **暂存**：`git add .` (将已修改的文件标记为待提交状态)
3. **记录**：`git commit -m "feat: 描述"` (正式保存改动，建议遵循常规提交规范)
4. **推送**：`git push` (将本地最新的存档提交同步到云端仓库)

---

## 三、 🌿 分支管理与现代切换 (Git 2.23+)
1. **切换分支**：`git switch [分支名]` (现代推荐：专门用于切换现有分支)
2. **新建并切换**：`git switch -c [分支名]` (现代推荐：创建并切换到新分支)
3. **撤销文件**：`git restore [文件名]` (现代推荐：将文件恢复到上次提交的状态)
4. **新建分支**：`git checkout -b [分支名]` (传统方式：创建新分支并立即切换过去)
5. **重命名分支**：`git branch -m [新名称]` (修改当前本地分支的名称)
6. **设置上游**：`git branch --set-upstream-to=origin/[远程分支]` (绑定本地与远程分支)
7. **推送分支**：`git push -u origin [分支名]` (将新分支推送到远程并建立关联)
8. **查看分支**：`git branch -a` (显示本地和远程所有已知的分支)
9. **删除本地分支**：`git branch -d [分支名]` (安全删除已合并的分支)
10. **删除远程分支**：`git push origin --delete [分支名]` (从 GitHub 服务器上彻底移除分支)

---

## 四、 🤝 PR 协作流程与合并策略
1. **Fork 工作流**：在 GitHub 网页点击 Fork，克隆到个人空间后再进行开发。
2. **创建 PR**：在 GitHub 网页发起 Pull Request，请求将你的分支合并到主仓库。
3. **普通合并**：`git merge [分支名]` (保留全部分叉历史的合并)
4. **无快速合并**：`git merge --no-ff [分支名]` (强制生成一个合并节点，方便追溯)
5. **变基合并**：`git rebase [分支名]` (将当前改动移至目标分支最新点之后，保持直线历史)
6. **Squash Merge**：GitHub 常用策略，将 PR 中的所有提交合并为一个整洁的提交。
7. **冲突状态**：`git status` (在冲突产生后查看哪些文件需要手动处理)
8. **继续流程**：`git rebase --continue` (解决冲突并 add 后，让合并继续进行)
9. **终止操作**：`git rebase --abort` (彻底放弃当前的合并/变基，回到操作前状态)

---

## 五、 📥 Stash 临时储藏管理
1. **存入储藏**：`git stash` (将未完成的改动暂时存入“后台”，让工作区变干净)
2. **查看列表**：`git stash list` (查看所有存入后台的临时记录)
3. **取出并删除**：`git stash pop` (将最近一次存入的内容取回到工作区并删除记录)
4. **应用不删**：`git stash apply` (仅取回内容，保留储藏记录)
5. **清空储藏**：`git stash clear` (删除所有存入后台的临时记录)

---

## 六、 🔧 Rebase 与历史修剪 (进阶)
1. **交互式变基**：`git rebase -i HEAD~n` (修改/合并/删除最近 n 次提交的历史)
2. **修正最后一次**：`git commit --amend` (将当前修改补入上次提交，并可修改备注)
3. **安全强推**：`git push --force-with-lease` (比 -f 更安全，若远程有新提交则拒绝强制覆盖)
4. **强制推送**：`git push -f` (在修改历史 ID 后，强制覆盖云端仓库，慎用)

---

## 七、 🏷️ Tag、Release 与 CI/CD
1. **轻量标签**：`git tag [v1.0]` (在当前提交点打上一个简单的版本标记)
2. **附注标签**：`git tag -a [v1.0] -m "说明"` (创建包含备注、日期和签名的正式标签)
3. **推送标签**：`git push origin --tags` (将所有本地标签一次性同步至 GitHub)
4. **发布 Release**：在 GitHub 网页端基于 Tag 发布 Release 并挂载成品文件。
5. **GitHub Actions**：在 `.github/workflows/` 下配置 YAML 文件，实现自动测试与发布。
6. **语义化版本**：遵循 SemVer (v大版本.次版本.修订号)，如 v1.2.3。

---

## 八、 🧐 审计、差异与精准控制
1. **查看状态**：`git status` (实时体检：检查文件追踪情况)
2. **图形日志**：`git log --oneline --graph --all` (彩色图形化显示所有提交脉络)
3. **代码追责**：`git blame [文件名]` (显示每一行代码的作者和最后修改日期)
4. **交互式暂存**：`git add -p` (分块检查代码，决定每一小段是否加入暂存区)
5. **撤销暂存**：`git reset HEAD [文件名]` (将误加的文件从暂存区撤回)
6. **分叉差异**：`git diff main..feature` (比较两个分支之间的代码差异)
7. **生成补丁**：`git format-patch -1 [ID]` (将某次提交生成为 .patch 文件)

---

## 九、 🔗 远程管理、子模块与 LFS
1. **查看远程**：`git remote -v` (显示当前关联的 GitHub 仓库地址)
2. **修改地址**：`git remote set-url origin [URL]` (更新仓库对应的远程网址)
3. **添加子模块**：`git submodule add [URL]` (在仓库中嵌套另一个仓库)
4. **初始化子模块**：`git submodule update --init --recursive` (克隆后同步子模块内容)
5. **大文件管理**：`git lfs track "*.psd"` (使用 Git LFS 追踪并管理超大二进制文件)
6. **Access Token**：使用 GitHub PAT (Personal Access Token) 代替密码进行安全认证。

---

## 十、 🔐 安全、Hooks 与签名
1. **SSH Key**：`ssh-keygen -t rsa -b 4096` (生成用于 GitHub 免密登录的密钥对)
2. **SSH 签名**：最新规范，支持使用 SSH Key 替代 GPG 进行提交签名认证。
3. **签名提交**：`git commit -S -m "signed"` (使用密钥为提交内容进行加密签名)
4. **本地 Hooks**：`.git/hooks/` (在此目录下存放脚本，实现提交前自动检查代码)
5. **保护分支**：在 GitHub 设置 Protected Branch，禁止强制推送并要求 PR 评审。

---

## 十一、 🚑 异常恢复与仓库治理
1. **操作回放**：`git reflog` (查看所有历史操作记录，用于寻找被删除的提交)
2. **恢复分支**：`git checkout -b [新名] [ID]` (根据 reflog 找到的 ID 恢复误删的分支)
3. **拣选提交**：`git cherry-pick [ID]` (精准地将另一个分支的某次提交合并到当前分支)
4. **仓库瘦身**：`git gc --prune=now` (清理不再需要的对象，优化仓库性能)
5. **完整性检查**：`git fsck` (验证数据库中对象的连通性和有效性)
6. **取消追踪**：`git rm --cached [文件名]` (将已追踪的文件从仓库移除但保留本地磁盘文件)

---

## 十二、 📚 仓库治理规范 (工程化建议)
* **工作流模型**：推荐使用 **GitHub Flow** (简单分支 -> PR -> 合并) 或 **Git Flow**。
* **README 规范**：应包含项目简介、安装指南、使用示例及贡献指南。
* **License**：必须包含 LICENSE 文件明确版权规则。
* **Issue 模板**：在 `.github/ISSUE_TEMPLATE/` 下配置，规范 Bug 反馈格式。

---
*Created by: noexemption*