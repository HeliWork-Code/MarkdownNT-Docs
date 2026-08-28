# MarkdownNT 开发指南

本指南帮助你搭建开发环境、运行项目并了解代码结构。

## 环境要求

- **.NET SDK**：8.0 或更高版本
- **操作系统**：Windows、macOS、Linux
- **IDE**：Visual Studio 2022 或 VS Code（推荐安装 C# 扩展）

## 获取代码

```bash
git clone https://github.com/你的用户名/MarkdownNT.git
cd MarkdownNT
```

## 运行项目

```bash
dotnet run
```

如果使用 Visual Studio，直接打开解决方案文件 `MarkdownNT.sln` 并点击运行。

## 构建

```bash
dotnet build
```

## 项目结构

```
MarkdownNT/
├── App.axaml                 # 应用程序资源与主题
├── App.axaml.cs              # 应用入口逻辑
├── MainWindow.axaml          # 主窗口布局
├── MainWindow.axaml.cs       # 主窗口交互与预览逻辑
├── MarkdownRenderer.cs       # 渲染代码块等复杂块
├── CodeHighlighter.cs        # 代码语法高亮
├── HtmlExporter.cs           # 导出为 HTML
├── ViewModels/               # 视图模型（如有）
├── Assets/                   # 资源文件
└── spec.md                   # 格式规范文档
```

## 关键代码说明

### MainWindow.axaml.cs

包含核心的 Markdown 解析与预览更新逻辑。`UpdatePreview` 方法逐行解析输入文本，并根据语法生成对应的 Avalonia 控件。

### MarkdownRenderer.cs

负责渲染代码块。你可以在这里调整代码块样式或添加新的块类型渲染。

### CodeHighlighter.cs

为代码块提供基础语法高亮，目前支持 Python 和 C#。若要添加新语言，在 `HighlightCode` 方法中增加关键字列表即可。

### HtmlExporter.cs

将 MarkdownNT 文本转换为 HTML，用于导出。若需修改导出样式，编辑其中的 CSS 字符串。

## 测试

目前项目未包含自动化测试。手动测试时请覆盖：
- 标题、列表、引用、分割线
- 加粗、斜体、行内代码
- 代码块（开始、结束、语言标签）
- 表格
- 主题切换
- 文件打开、保存、自动保存
- HTML 导出

## 常见问题

### 编译慢或文件占用

- 关闭 Visual Studio 的 Avalonia 设计器预览
- 将项目放在本地 SSD
- 将项目文件夹加入杀毒软件排除列表

### 加粗/斜体预览不生效

- 该问题已在 Avalonia 12.1.1 中发现，可能需降级到 Avalonia 11.0.10
- 暂时可通过导出 HTML 验证格式正确性

### 找不到 Avalonia 模板

在命令行运行：
```bash
dotnet new install Avalonia.Templates
```

## 开发流程建议

1. 从 `MainWindow.axaml.cs` 开始了解解析流程
2. 修改代码后运行 `dotnet run` 测试
3. 提交前确保无编译错误
4. 遵循现有代码风格，使用清晰命名

## 获取帮助

- 在 GitHub Issues 提问
- 查看 [格式规范](spec.md) 了解语法设计
