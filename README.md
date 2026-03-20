# text-card-skills

用于生成文字卡片图片的技能仓库。

目前包含两个 skill：

- `text-card`：基于模板或参考示例生成卡片 HTML
- `html-to-image-render`：将本地 HTML 渲染为 PNG / JPEG

## 目录

```text
skills/
  text-card/
  html-to-image-render/
```

## 用法

1. 在 `skills/text-card/` 中选择模板或示例，修改文案。
2. 确保卡片容器为 `id="card"`。
3. 运行渲染脚本输出图片：

```bash
mkdir -p text-card-images

npx -y tsx skills/html-to-image-render/scripts/render-html-to-image.ts \
  --input skills/text-card/references/example-quote-text-card-blue.html \
  --output text-card-images/example.png \
  --element-id card \
  --image-type png
```

## 要求

- 本机可用 `node` 和 `npx`
- 需要能访问 `https://html2image.hanfangyuan.cn`

## 说明

- 默认建议复用 `skills/text-card/references/` 下的示例，而不是从零制作
- 输出目录建议使用 `text-card-images/`，该目录已被 `.gitignore` 忽略
- 如果截图被裁切，增大 `--viewport-width` 和 `--viewport-height`
