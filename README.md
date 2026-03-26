# text-card-skills

用于生成文字卡片图片的 Claude Code 技能集，适用于小红书、公众号等图文场景。

## 前置要求

- 已安装 Node.js 环境
- 能够运行 `npx` 命令
- 网络可访问 `https://html2image.hanfangyuan.cn`

## 安装

### 快速安装（推荐）

```bash
npx skills add hanfangyuan4396/text-card-skills
```

### 注册插件市场

在 Claude Code 中运行：

```
/plugin marketplace add hanfangyuan4396/text-card-skills
```

### 安装技能

**方式一：通过浏览界面**

1. 选择 **Browse and install plugins**
2. 选择 **text-card-skills**
3. 选择 **Install now**

**方式二：直接安装**

```
/plugin install text-card-skills@text-card-skills
/reload-plugins
```

/reload-plugins 可能无效，可能需要重启 Claude Code，插件才能生效

**方式三：告诉 Agent**

直接告诉 Claude Code：

> 请帮我安装 github.com/hanfangyuan4396/text-card-skills 中的 Skills

## 可用插件

| 插件 | 说明 | 包含内容 |
|------|------|----------|
| text-card-skills | 文字卡片生成与 HTML 转图片技能 | 仓库中的全部 skills，按下方分类展示 |

## 更新技能

更新技能到最新版本：

1. 在 Claude Code 中运行 `/plugin`
2. 切换到 **Marketplaces** 标签页（使用方向键或 Tab）
3. 选择 **text-card-skills**
4. 选择 **Update marketplace**

也可以选择 **Enable auto-update** 启用自动更新，每次启动时自动获取最新版本。

## 可用技能

### 内容技能

| 技能 | 说明 |
|------|------|
| `text-card` | 制作文字卡片图片，优先基于模板和示例生成卡片 HTML，适用于小红书卡片、公众号配图等场景 |

### 工具技能

| 技能 | 说明 |
|------|------|
| `html-to-image-render` | 将本地 HTML 文件通过远端 API 渲染为 PNG / JPEG 图片 |

## 用法示例

直接使用 `/text-card` 命令，让 Agent 自动帮你生成卡片：

```
/text-card 你的卡片文案内容
```

例如：
```
/text-card 加入方圆AI社区，了解AI工具、通俗易懂的方法和实践内容
```

Agent 会基于模板自动生成 HTML 并渲染为图片，保存到 `text-card-images/` 目录。

### 示例效果

| HTML 源文件 | 渲染图片 |
|-------------|---------|
| [fangyuan-ai-community.html](docs/htmls/fangyuan-ai-community.html) | ![fangyuan-ai-community](docs/images/fangyuan-ai-community.png) |

## 目录结构

```text
skills/
  text-card/                    # 文字卡片技能
    SKILL.md
    assets/                     # 卡片模板
    references/                 # 参考示例
  html-to-image-render/         # HTML 转图片技能
    SKILL.md
    assets/                     # 示例 HTML
    references/                 # API 文档
    scripts/                    # 渲染脚本
```

## 注意事项

- 默认建议复用 `skills/text-card/references/` 下的示例，而不是从零制作
- 输出目录建议使用 `text-card-images/`，该目录已被 `.gitignore` 忽略
- 如果截图被裁切，增大 `--viewport-width` 和 `--viewport-height`
- HTML 中的图片资源需要使用公网可访问的链接，不支持本地图片路径
