---
title: "git tag"
sequence: 'tag'
---

## 查看 tag

```text
git tag
# 或
git tag --list
```

```text
git show <tagName>
```

## 添加 tag

```text
git tag <tagName>
git tag <tagName> <commitId>
```

示例：

```text
$ git tag v2023.01
$ git tag --list
v2023.01
```

## 删除 tag

```text
git tag --delete <tagName>
```

示例：

```text
$ git tag --delete v2023.01
Deleted tag 'v2023.01' (was 30d5061)
```

## 推送 tag

从 local 向 remote 推送 tag：

```text
git push --tags
```

示例：

```text
$ git push --tags
warning: redirecting to http://36.138.170.6:8929/bdjm/jm-dma-service.git/
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
To http://36.138.170.6:8929/bdjm/jm-dma-service
 * [new tag]         v2023.01 -> v2023.01
```

## 拉取 tag

在 local 从 remote 拉取 tag：

```text
git fetch
```
