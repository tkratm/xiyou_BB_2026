# 碧波烬 · 工作记录板

> GitHub Pages 独立部署 · 全平台自动同步 · 专业级项目管理

**在线地址**：`https://[你的用户名].github.io/xiyou-workboard/`

---

## 功能

| 视图 | 说明 |
|------|------|
| 📋 **看板** | 三列（待开始/进行中/已完成），点卡片进阶段详情 |
| 📅 **日历** | 月度视图 + 里程碑标记，点标记直跳到看板对应阶段 |
| 🖼️ **素材库** | 全部阶段的所有图片/视频一览 |
| ⚙️ **阶段详情** | 任务清单可勾选 + 备注可添加 + 拖放上传图片/视频 |

**数据同步方案**：
- GitHub 仓库作为"数据库"，`data.json` 存所有任务/备注/状态
- 上传的图片/视频通过 GitHub API 存到 `uploads/` 目录
- 任何设备打开同一个 URL → 自动同步（手动点「同步」按钮）

---

## 部署步骤（5 分钟）

### 1. 创建 GitHub 仓库

去 [github.com/new](https://github.com/new) 创建新仓库：
- **仓库名**：`xiyou-workboard`
- **类型**：**Public**（公开）
- 不要勾选 "Add a README file"

### 2. 创建 Personal Access Token

去 [github.com/settings/tokens/new](https://github.com/settings/tokens/new)：
- **Note**：`xiyou-workboard`
- **Expiration**：自定义（建议 90 天）
- **勾选**：`public_repo` （如果仓库公开）或 `repo`（如果私有）
- 点「Generate token」→ **复制 token 保存好**（只显示一次）

### 3. 推送文件到 GitHub

```bash
cd xiyou-workboard
git init
git add .
git commit -m "初始版本：碧波烬工作记录板"
git branch -M main
git remote add origin https://github.com/[你的用户名]/xiyou-workboard.git
git push -u origin main
```

### 4. 启用 GitHub Pages

1. 仓库页面 → **Settings** → **Pages**
2. **Source**：选 `Deploy from a branch`
3. **Branch**：选 `main`，文件夹选 `/ (root)`
4. 点 **Save**
5. 等 1-2 分钟，页面顶部会显示你的 URL：
   `https://[你的用户名].github.io/xiyou-workboard/`

### 5. 配置连接

1. 打开你的 GitHub Pages URL
2. 点右上角 **⚙️** 打开设置
3. 填入：
   - **GitHub 用户名**：你的 GitHub 用户名
   - **仓库名**：`xiyou-workboard`
   - **Token**：刚才复制的 token
4. 点「测试连接」确认
5. 成功后点「同步」拉取初始数据

---

## 日常使用

### 电脑/手机/家/公司 → 同一 URL

收藏 `https://[你的用户名].github.io/xiyou-workboard/`，任何设备浏览器打开就是最新的。

### 同步操作

- **拉取最新**：打开页面自动读取 `data.json`
- **推送修改**：改完后点右上角 `🔄 同步` → 数据写回 GitHub
- **自动同步**：配置好 GitHub 连接后，每次打开页面会自动同步

### 上传素材

1. 打开某个阶段的详情
2. 拖放图片/视频到上传区域
3. 文件自动上传到 GitHub 仓库的 `uploads/` 目录
4. 所有设备都能看到

### 导出/导入（离线备份）

- **导出**：设置面板 → `📥 导出本地备份` → 下载 JSON
- **导入**：设置面板 → `📤 导入本地备份` → 选 JSON 文件

---

## 文件结构

```
xiyou-workboard/
├── index.html        ← 完整应用（HTML+CSS+JS）
├── data.json         ← 数据文件（任务/备注/状态/素材索引）
├── uploads/          ← 上传的图片/视频
└── README.md
```

---

## 技术说明

- 纯浏览器端应用，无服务端依赖
- 数据存储：GitHub 仓库 `data.json` + 浏览器 localStorage 缓存
- 同步协议：GitHub REST API v3
- 图片/视频：上传到 GitHub 仓库 `uploads/` 目录，通过 raw.githubusercontent.com 加载
