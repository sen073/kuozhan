# 笔趣阁 m.bqglll.cc · Legado 书源

面向开源阅读 / Legado 的书源配置，目标站点：`https://m.bqglll.cc/`

> 本仓库目录只提供**规则配置**，不提供任何小说正文。  
> 请遵守法律法规与站点条款，仅供学习书源规则使用。

## 位置

GitHub 目录：

https://github.com/sen073/kuozhan/tree/main/legado-bqglll

## 网络导入链接（推荐）

```text
https://raw.githubusercontent.com/sen073/kuozhan/main/legado-bqglll/booksource.json
```

## 手机导入

### 方式 A：网络导入
1. 打开 **阅读 / Legado**
2. **我的 → 书源管理**
3. 右上角 **三点 → 网络导入**
4. 粘贴上面的 raw 链接 → 确定
5. 确认书源 **笔趣阁m.bqglll** 已启用

### 方式 B：本地导入
1. 下载 `booksource.json`
2. **书源管理 → 本地导入 → 选文件**

### 方式 C：剪贴板
1. 复制 `booksource.json` 全文
2. **书源管理 → 新建/剪贴板导入**

## 使用

1. 书架右上角 **搜索**
2. 先试：`剑来`、`凡人`、`斗破苍穹`
3. 或打开 **发现**，按分类浏览
4. 进入书籍 → 点目录 → 阅读

### 调试

书源管理 → 点该源 → 编辑 → 右上角 **调试**  
搜索词填 `剑来`，看搜索/详情/目录/正文哪一步失败。

常见情况：
- 搜索返回空：站点接口不稳定，换词或用发现页
- AES 报错：需要较新的阅读 3.x
- 已知书籍页：复制 `https://m.bqglll.cc/look/数字/` 用“添加网址”

## 技术链路

```text
搜索  m.bqglll.cc/user/search.html?q=
详情  m.bqglll.cc/look/{id}/  → 解析 bid
目录  apibi.cc/api/booklist?token=AES({"id":bid})
正文  apibi.cc/api/chapter?token=AES({"id":bid,"chapterid":n})
```

Token：
1. `md5 = MD5("book@token.html")`
2. `iv = md5[0:16]`，`key = md5[16:32]`
3. `AES/CBC/PKCS5Padding` 后 Base64

## 免责

站点内容混杂，请自行甄别；支持正版。
