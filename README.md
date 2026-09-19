# 定向越野模拟游戏 (Orienteering Game)

这是一个基于 Twine / SugarCube 2.37.3 引擎开发的沉浸式定向越野模拟游戏。玩家将扮演参赛者，在鼓浪屿的地图背景下，根据提示与检查点说明表，在不同控制点选择最优路线，并通过附加题获得加分。

## 🌟 游戏特性

- **多语言支持**：全游戏支持简体中文与英文的无缝切换。
- **双模式难度**：
  - **小白模式**：满分 100 分，侧重于基础路线选择与计分。
  - **老手模式**：满分 200 分，包含隐藏的附加题与进阶附加题（考验路线记忆与图例识别）。
- **动态路线选择**：每个控制点提供红、蓝、橙、棕等不同颜色的路线选项，不同路线对应不同分值。
- **历史排行榜**：游戏结束时记录成绩，并按分数降序排列。排行榜设计为**跨局保留**（方便玩家连续挑战），在点击自定义“重新开始”时不会清空。
- **交互式地图查看**：侧边栏提供“查看大图”功能，支持鼠标滚轮缩放与拖拽平移（针对 PC 端优化），方便玩家查看细节。
- **视觉小说式对话**：内置自定义的 `<<speech>>` 宏，以卡片气泡样式展示角色对话。

## 🛠️ 技术栈与架构

- **引擎**: Twine / SugarCube 2.37.3
- **语言**: HTML / CSS / JavaScript (内置宏与自定义 JS 扩展)
- **核心模块划分**:
  - `StoryInit`: 全局状态初始化。
  - `Lang_ZH` / `Lang_EN`: 双语文本与配置分离。
  - `Points_Data`: 数据驱动的关卡配置（控制点、路线选项、分值）。
  - `StoryScript`: 自定义 JS 宏（`speech` 对话渲染、`setupMapZoom` 地图缩放逻辑）。
  - `StoryStylesheet`: 全局样式与响应式布局。
  - `RenderPoint`: 通用控制点渲染组件（动态加载图片与生成路线按钮）。
  - `Finish`: 结算与排行榜逻辑。

## 🚀 如何运行

1. 确保你已安装 Twine 2 编辑器，或者使用 Tweego 等命令行工具。
2. 将 `Orienteering.twee` 文件导入 Twine，或直接编译。
3. 如果已有导出的 `.html` 文件，直接使用现代浏览器（Chrome / Edge / Firefox）双击打开即可运行。
4. **注意**：游戏素材依赖于 `img/` 文件夹下的资源。请确保同级目录下包含 `img/blank/`、`img/route/`、`img/icon.jpg`、`img/you.jpg`、`img/CDS.jpg`、`img/map.jpg`、`img/scene.jpg`、`img/extra.jpg`、`img/QRcode.jpg` 等文件。

## 📝 维护与扩展指南

- **增加新控制点**：只需在 `Points_Data` 段落中按照现有对象结构添加新的 ID，并在 `PtX` 段落中调用 `<<renderPoint X>>`。无需修改 `RenderPoint` 核心逻辑。
- **增加新路线颜色**：如果需要在 `Points_Data` 中使用新的 `labelKey`（如 `purple`），只需在 CSS 中新增 `[data-route="purple"]` 的样式，系统会自动接管渲染。
- **修改题目内容**：可直接在 `Lang_ZH` 与 `Lang_EN` 中修改对应的 `$t_bonus_*` 或 `$t_extra_*` 变量。

---
*Developed for SUSTech Orienteering Club.*
