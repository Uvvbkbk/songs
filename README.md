# 我会唱的歌

一个纯前端的个人歌单 / 卡拉 OK 点歌助手。页面使用原生 HTML、CSS 和 JavaScript，不需要 Node.js 或构建工具。

## 功能

- 按分类展示歌曲，并支持分类折叠、重命名和管理。
- 搜索歌名与标签，按歌名或标签排序，随机选曲并复制歌名。
- 使用标签筛选歌曲，支持编辑标签。
- 管理模式下可新增、编辑、删除歌曲，并通过 CSV 导入或导出歌单。
- 多种主题、樱花动画，以及可配置的 Bilibili、YouTube、Niconico 搜索入口。
- 歌单数据通过 GitHub Gist API 读取和保存。

## 运行

直接在浏览器中打开 `index.html` 即可；也可以通过 GitHub Pages 等静态网站服务发布。项目没有构建步骤。

## 配置歌单数据

打开 `index.html`，找到脚本顶部的 `CONFIG`：

```js
const CONFIG = {
  GIST_ID: '你的 Gist ID',
  FILE_NAME: 'songs.json',
};
```

指定的 Gist 中需要存在 `songs.json`。文件内容应为 JSON 数组，每首歌曲可包含以下字段：

```json
[
  {
    "id": "song-001",
    "title": "歌曲名称",
    "category": "分类名称",
    "tags": ["标签一", "标签二"]
  }
]
```

页面会通过 GitHub API 读取 Gist。若要新增或修改云端歌单，请点击页面头像进入管理模式，并提供具有所需 Gist 权限的 GitHub Personal Access Token。

## 安全提示

- **不要把 Personal Access Token 写进代码或提交到仓库。**
- 当前页面会把 Token 保存在浏览器的 `localStorage` 中，方便下次登录；同一浏览器来源下的脚本可访问它。请只在可信设备上使用，并避免在公用电脑登录。
- Token 会直接发送给 GitHub API 用于验证和写入，不会通过本项目的自建后端中转。
- 建议为 Token 设置有效期，并仅授予完成 Gist 操作所需的最小权限。使用完毕后，可在 GitHub 设置中撤销 Token；清除浏览器站点数据也会删除本地保存的 Token。
- Gist 的可见性由 GitHub 上该 Gist 自身的设置决定。请不要把私密信息放入公开 Gist。

## 项目结构

- `index.html`：页面结构、样式、交互逻辑和 GitHub Gist API 调用。
- `manifest.json`：安装为网页应用时使用的 Web App Manifest。

## 已知限制

这是一个单页静态应用，Token 管理和数据访问都在浏览器中完成；它没有独立后端、自动化测试套件或构建流程。若未来要供多人使用，建议改为带服务端身份验证的架构，而不是共享个人访问令牌。
