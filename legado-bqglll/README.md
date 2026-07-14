# 笔趣阁 m.bqglll.cc · Legado 书源

面向 [开源阅读 / Legado](https://github.com/gedoor/legado) 的书源配置，目标站点：

- 入口：`https://m.bqglll.cc/`
- 搜索：`/user/hm.html` + `/user/search.html`
- 详情：`/look/{id}/`
- 目录/正文：`https://apibi.cc/api/*`（AES token）

> 本仓库只提供**规则配置**，不提供任何小说正文内容。  
> 请遵守当地法律法规与目标站点条款，仅供学习研究书源规则使用。

## 文件

| 文件 | 说明 |
|---|---|
| `booksource.json` | 可直接导入的书源（JSON 数组） |
| `raw/笔趣阁m.bqglll.json` | 单书源对象（便于阅读） |

## 一键导入（网络）

把下面链接导入阅读 App（需可访问 GitHub raw）：

```text
https://raw.githubusercontent.com/sen073/legado-booksource-bqglll/main/booksource.json
```

## 手机导入步骤

### 方式 A：网络导入
1. 打开 **阅读 / Legado**
2. 右下角 **我的 → 书源管理**
3. 右上角 **☰ / 三点 → 网络导入**
4. 粘贴上面的 raw 链接 → 确认导入
5. 确保书源 **已启用**

### 方式 B：本地文件导入
1. 下载本仓库的 `booksource.json` 到手机
2. **我的 → 书源管理 → 本地导入**
3. 选择该文件

### 方式 C：剪贴板导入
1. 复制 `booksource.json` 的全部内容
2. **书源管理 → 新建 / 剪贴板导入**

## 使用

1. 回到书架，点右上角 **搜索**
2. 建议先试关键词：`剑来`、`凡人`、`斗破苍穹`
3. 也可在 **发现** 里按分类浏览（玄幻/武侠/都市…）
4. 点进书籍 → 目录 → 开始阅读

### 调试（搜不到/目录空时）

1. 书源管理 → 点这本书源 → 编辑  
2. 右上角 **调试**  
3. 搜索词填 `剑来`  
4. 查看搜索 / 详情 / 目录 / 正文哪一步失败

常见情况：
- 搜索偶发返回 `[]`：站点接口不稳定，换词或稍后再试；也可用 **发现** 分类进入
- AES 报错：确认 App 为较新的阅读 3.x，并支持 `java.aesEncodeToBase64String`
- 只想读某一本：可直接用浏览器打开书籍页，复制 `https://m.bqglll.cc/look/xxxxx/`，在阅读里 **添加网址**

## 技术说明（架构）

```text
搜索: m.bqglll.cc/user/search.html?q=关键词
  ↑ 需先访问 hm.html 写 cookie，并带 getsite

详情: m.bqglll.cc/look/{lookId}/
  → 解析 addBookCase('bid') 得到内部书籍 ID

目录: GET apibi.cc/api/booklist?token=AES({"id":"bid"})
  → list: ["第1章…","第2章…", ...]

正文: GET apibi.cc/api/chapter?token=AES({"id":bid,"chapterid":n})
  → $.txt
```

Token 算法：
1. `md5 = MD5("book@token.html")`（32 位 hex）
2. `iv = md5[0:16]`，`key = md5[16:32]`（按 UTF-8 字节作 AES-128）
3. `token = Base64(AES/CBC/PKCS5Padding(JSON payload))`

## 免责声明

- 书源规则为公开网页/接口的解析描述，不存储作品正文
- 站点本身内容混杂，可能含成人向或侵权转载内容
- 请支持正版；因使用本规则产生的任何后果由使用者自行承担
