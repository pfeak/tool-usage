# Git 常用命令

## 参考

[Git 不要只会 pull 和 push，试试这 5 条提高效率的命令](https://mp.weixin.qq.com/s/mhi4RNLzA5nzDPTBe36mUw)

## 默认编辑器

设置 vim 为默认 git 命令编辑器：`git config --global core.editor vim`

## stash

| 作用                                 | 命令                        |
| ------------------------------------ | --------------------------- |
| 保存当前未 commit 的代码             | git stash                   |
| 保存当前未 commit 的代码并添加备注   | git stash save "备注的内容" |
| 列出 stash 的所有记录                | git stash list              |
| 删除 stash 的所有记录                | git stash clear             |
| 应用最近一次的 stash                 | git stash apply             |
| 应用最近一次的 stash，随后删除该记录 | git stash pop               |
| 删除最近的一次 stash                 | git stash drop              |

## reset

| 作用                 | 命令                         |
| -------------------- | ---------------------------- |
| 恢复 commit 保留代码 | git reset --soft "commit id" |
| 恢复 commit          | git reset --hard "commit id" |

## cherry-pick

| 作用                             | 详细                        | 命令                               |
| -------------------------------- | --------------------------- | ---------------------------------- |
| 从其他分支复制 commit 到当前分支 | 复制单条 commit             | git cherry-pick commit1            |
|                                  | 复制多条 commit             | git cherry-pick commit1 commit2    |
|                                  | 复制多条 commit             | git cherry-pick commit1^...commit2 |
| 代码冲突解决                     | 解决冲突暂存后继续          | git cherry-pick --continue         |
|                                  | 放弃复制，恢复到最开始状态  | git cherry-pick --abort            |
|                                  | 放弃复制，保留已复制 commit | git cherry-pick --quit             |

