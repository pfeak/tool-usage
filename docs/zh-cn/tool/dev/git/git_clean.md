# Git 清空 unversioned files

## 故事背景

有一个 go 的项目仓库，需要经常切换分支，由于历史原因 `pkg/mod/cache/download` 放在项目目录下，每次 go tidy 会导致许多库被 git 标记为 `unversioned files`，这样很不美观，所以想清理掉这些没有 git 追踪的文件。

```bash
➜  ls
target_file.zip

➜  git status
On branch dev
Your branch is up to date with 'origin/dev'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        target_file.zip

nothing added to commit but untracked files present (use "git add" to track)
```

## git clean

|参数|说明|
|:-:|:-:|
|-d|指定路径，递归删除|
|-f|强制执行|
|-n, --dry-run|不会真正删除，仅展示将如何执行|

执行递归删除，先查看将会如何执行，避免误删

```shell
➜  git clean -dfn 
Would remove target_file.zip
```

真实执行删除

```shell
➜  git clean -df 
Removing target_file.zip
```

查看 git 状态

```shell
➜  git status   
On branch dev
Your branch is up to date with 'origin/dev'.

nothing to commit, working tree clean
```