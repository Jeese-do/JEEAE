# 生图 Skills

这个文件夹收录了两个用于 GPT 生图的 Agent Skill（适用于 Claude Code / Codex / Cursor 等支持 skills 的 Agent），主打两个用途：

1. **更换人物场景 / 换背景**（保持人物不变，只换环境）
2. **去除 AI 感**（写实摄影风格的提示词模板）

## 目录

### `gpt-image-2/` — 生图 / 改图主力 Skill

来源：[ConardLi/garden-skills](https://github.com/ConardLi/garden-skills)（MIT 许可）

面向 GPT Image 2 的结构化生图/编辑技能，18 大类、80+ 模板。和本需求最相关的模板在 `references/editing-workflows/`：

| 模板 | 用途 |
|---|---|
| `background-replacement.md` | **人像/商品换背景**：主体不动，把人放进新场景（棚景/户外/生活场景） |
| `portrait-local-edit.md` | 人像局部编辑，保持人物身份一致 |
| `object-removal.md` | 去除画面中的路人/杂物 |
| `local-object-replacement.md` | 局部物体替换 |

三种运行模式（详见 `gpt-image-2/SKILL.md`）：

- **Mode A**：配置 `OPENAI_API_KEY` + `ENABLE_GARDEN_IMAGEGEN=1`，直接用 `scripts/generate.js` / `scripts/edit.js` 调 API 出图落盘
- **Mode B**：作为提示词工程指引，把渲染好的 prompt 交给宿主 Agent 的图像工具
- **Mode C**：纯提示词顾问，只产出高质量 prompt

换背景示例（Mode A）：

```bash
node 生图/gpt-image-2/scripts/edit.js --image 原图.jpg --prompt "参照 background-replacement 模板写好的提示词"
```

### `gpt-image-2-style-library/` — 写实风格库（去 AI 感）

来源：[freestylefly/awesome-gpt-image-2](https://github.com/freestylefly/awesome-gpt-image-2)（MIT 许可）

470+ 逆向工程案例提炼的风格库，`references/style-library.md` 里包含"摄影与现实主义"类风格（镜头焦段、自然光线、逼真皮肤纹理），用来给生图 prompt 叠加写实质感、消除 AI 味。

## 安装为 Claude Code Skill

把两个文件夹拷到 skills 目录即可（项目级或全局二选一）：

```bash
# 项目级
mkdir -p .claude/skills
cp -r 生图/gpt-image-2 生图/gpt-image-2-style-library .claude/skills/

# 或全局
cp -r 生图/gpt-image-2 生图/gpt-image-2-style-library ~/.claude/skills/
```

重启 Agent 会话后生效。

## 去 AI 感速查

无论用哪个模板，往 prompt 里加真实相机语言效果最直接：

- 具体镜头与焦段：`shot on 35mm lens, f/1.8`
- 自然光与瑕疵：`natural window light, slight film grain`
- 真实纹理：`realistic skin texture, visible pores, no beauty filter`
- 随手拍质感：`candid, unedited, shot on iPhone`
- 不完美构图：`slightly off-center composition`

## 许可

两个 skill 均为 MIT 许可，各自目录内保留了原仓库的 `LICENSE` 文件。
