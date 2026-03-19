---
name: text-card
description: 当需要制作文字卡片图片时使用，包括生成卡片 HTML，并调用底层 HTML 转图片能力输出最终图片。适用于小红书、公众号图文等场景，也适用于其他文字卡片图片生成任务。
---

# 文字卡片

当任务是制作文字卡片图片时，使用这个 skill。这个 skill 适合：

- 小红书卡片图或封面图
- 公众号图文配图或封面图
- 其他需要先生成 HTML 再导出图片的文字卡片场景

## 工作流

1. 收集卡片文案和基础样式信息。
2. 优先查看 `assets/` 中是否已有合适的 HTML 模板。
3. 有合适模板时，复制并修改模板内容；没有合适模板时，直接从零生成完整 HTML。
4. 确保最终 HTML 中有明确的卡片容器，推荐使用 `id="card"`。
5. 调用底层 `html-to-image-render` skill，把 HTML 渲染成图片。
6. 检查输出的 HTML 和图片文件。

## 模板使用

- `assets/` 目录下可以放文字卡片模板，供后续直接复制或改写。
- 如果用户提供了新的参考模板，优先在现有模板基础上调整，避免每次从零开始。
- 如果现有模板不适合当前需求，再直接生成新的完整 HTML。

当前可参考模板：

- `assets/summary-card-template.html`
- `assets/quote-text-card-template.html`

其中：

- `summary-card-template.html` 更适合内容摘要类文字卡片。
- `quote-text-card-template.html` 更适合引用式、大字号、单段正文高亮类卡片。

推荐配色（适用于 `quote-text-card-template.html` 当前版本）：

- 背景色：`#ede7fb`
- 正文字色：`#403d52`
- 引号/角标色：`#dfcef0`
- 高亮底色：`#f7be3f`

另一组可选推荐配色：

- 背景色：`#cef0ff`
- 引号/角标色：`#a3d5f2`
- 高亮底色：`#fdb8f6`
- 正文字色建议：`#2f3a4a`

说明：

- 上面这两组配色仅供参考，实际生成时可根据用户需求自由使用其他颜色。

版式约定：

- 一般使用纯色背景，默认不要额外加入渐变、光晕或大面积装饰背景。
- 如果用户明确要求更强的视觉氛围，再考虑加入轻量渐变或局部装饰效果。

## 生成要求

- 默认输出单张卡片布局，核心内容放在 `#card` 容器中。
- 优先保证文字层级清晰、留白稳定、截图边界明确。
- 适配小红书、公众号时，只把它们当作版式风格参考，不要把 skill 限定为某个平台专用。
- 如果需要远程图片、Logo、字体，预留足够的加载等待时间给底层渲染。

## 调用底层渲染

生成好 HTML 后，调用底层 `html-to-image-render` skill 的脚本进行渲染，例如：

```bash
npx -y tsx skills/html-to-image-render/scripts/render-html-to-image.ts \
  --input ./tmp/card.html \
  --output ./tmp/card.png \
  --element-id card \
  --image-type png
```

如果卡片里有远程资源，可以额外增加 `--render-wait-ms`。

## HTML 编写建议

- 使用内联 `style` 或 `<style>`，避免依赖外部样式文件。
- 明确设置背景、圆角、阴影、字体大小、行高和内边距。
- 标题不要过长，避免换行后破坏视觉重心。
- 正文、标签、品牌区等信息要有清晰层级。
- 如果内容较多，优先控制卡片宽度和段落节奏，而不是单纯缩小字号。
- 如果使用浅紫系引用卡片，可优先沿用 `#ede7fb / #403d52 / #dfcef0 / #f7be3f` 这一组配色。
- 引用卡片默认优先保持纯色背景和大字号正文，不要主动加复杂背景效果。

## 注意事项

- 这个 skill 不依赖独立脚本，重点是生成高质量 HTML。
- 图片输出依赖底层 `html-to-image-render` skill。
- 输出图片时，`--output-image` 的扩展名应与 `--image-type` 保持一致。
- 如果底层渲染报 `element_id` 不存在，先检查 HTML 中是否真的存在 `id="card"`。
