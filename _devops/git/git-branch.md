---
title: "git branch"
sequence: 'branch'
---

查看帮助：

```text
git help branch
```

## 本地分支

查看分支：

```text
git branch
```

创建本地 `dev` 分支：

```text
git branch dev
```

切换本地 `dev` 分支：

```text
git checkout dev
```

创建并切换到本地 `dev` 分支：

```text
git checkout -b dev
```

## 远程分支

查看远程分支：

```text
git branch -r
git branch --remotes
```

## 本地 -> 远程

将本地 `dev` 分支推送到远程 `origin/dev` 分支：

```text
git checkout dev
git push -u origin dev

或者

git checkout dev && git push -u origin dev
```

## 远程 -> 本地

根据远程 `origin/dev` 分支，创建 `local dev` 分支，并切换到 `local dev` 分支：

```text
git checkout -b dev origin/dev
```
