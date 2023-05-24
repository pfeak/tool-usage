# Git 修改已提交 commit 邮箱

## 1. 背景故事

由于在不同电脑设备上操作（每台设备 git 邮箱不一样），导致提交到 git 的邮箱不一致。



## 2. 修改原理

使用 `git rebase` 改变当前基础 commit，然后使用 `git commit --amend` 修改信息



## 3. 修改步骤

1. 指定需要修改的 commit（n 代表提交次数）

    ```shell
    git rebase -i HEAD~n
    ```

2. 此时进入 vi 或 vim 界面，按 `i` 进行编辑模式，将 `pick` 修改为 `edit`，按 `Esc` 退出编辑模式，按 `:wq` 保存退出。

3. 修改作者与邮箱（邮箱要带 `<`，`>`）

   ```shell
   git commit --amend --author="作者 <邮箱@xxx.com>" --no-edit
   ```


4. 提交修改

   ```shell
   git rebase --continue
   ```

5. 强制同步服务器

   ```shell
   git push --force
   ```




## 4. 参考

网页：[Git修改已经提交的用户名信息](https://www.cnblogs.com/tl542475736/p/11943718.html)
