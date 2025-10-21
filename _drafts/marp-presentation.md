---
marp: true
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
backgroundImage: url('https://marp.app/assets/hero-background.svg')
---

![bg left:40% 80%](https://marp.app/assets/marp.svg)

# **Marp**

Markdown Presentation Ecosystem

https://marp.app/

---

# How to write slides

Split pages by horizontal ruler (`---`). It's very simple! :satisfied:

```markdown
[!fit]
# Slide 1

foobar
·
---

# Slide 2

foobar
```
---
<!-- Page 1 --> 
Claude Code 个人使用心得

---

Part I  CLAUDE.md
是什么，怎么写

--- 
<!-- Page 1 --> 

Part II 场景

分几个场景来介绍：
- 开始全新项目的开发

- 对于接近开发完成项目的bug修复

- 拿到开源项目/别人开发完项目如何快速上手（比如deepwiki）

---

## 开始全新项目的开发
比如开发一个智能文档分析工具 SmartDoc Analyzer

CLAUDE.md
```markdown
# SmartDoc Analyzer - 开发规范

## 项目背景
基于 LLM 的智能文档分析系统，支持 PDF、Word、TXT 格式文档的智能解析和问答。

## 核心依赖
- **LLM**: OpenAI, Qwen, DeepSeek
- **文档解析**: PyPDF2, python-docx
- **向量数据库**: Milvus
- **Web框架**: FastAPI
- **异步处理**: asyncio, aiofiles
```
---
```
## 代码规范
### Python 类型提示
- 使用 PEP 604 联合类型: 使用 `str | None` 代替 `typing.Union` `typing.Optional`
- 使用 PEP 585 内置类型: 使用 `list[str]`, `dict[str, Any]` 代替 `typing.List`, `typing.Dict`

### 字符串和文档
- 字符串统一优先使用双引号
- docstring遵循 Google 风格

### 工具链
- 包管理: `uv`
- 代码格式化: `ruff`
- 测试: `pytest` + `pytest-asyncio`

### 项目结构（以下为参考项目结构，生成适合本项目的项目结构）
project-name/
│
├── src/                          # 核心功能（推荐使用具体名称，name_your_application）
│   ├── __init__.py
│   ├── __main__.py
│   ├── _config.py                # 项目配置文件
│   ├── feature_a.py              # 功能 A
│   ├── services/                 # 服务层 / API 接口实现
│   │   └── api_b.py              # API B
│   └── utils/                    # 通用工具模块
│       └── logger.py             # 日志配置
│
├── tests/                        # 测试套件
│   ├── __init__.py
│   ├── unit/                     # 单元测试
│   │   ├── test_feature_a.py
│   │   └── test_utils.py
│   ├── integration/              # 集成测试
│   │   └── test_services.py
│   ├── template.py               # 测试模板
│   │                             # import context
│   │                             # """Do not insert any code above!!!"""
│   └── context.py                # 测试上下文配置
│                                 # import sys
│                                 # from pathlib import Path
│                                 # sys.path.insert(0, Path(__file__).parents[1].absolute().__str__())
│
└── docs/                         # 项目文档
    ├── feature_a.md              # Feature A 详细说明
    ├── api_b.md                  # API B 的接口文档
    └── deployment.md             # 部署指南
```

---

开始使用claude
配置：ANTHROPIC_BASE_URL=, ANTHROPIC_AUTH_TOKEN=

实用的commands

/export 导出当前session记录
claude --resume  重新进入exit了的session
claude-code: how to output session /export

e.g. Code Refactoring and Modernization 代码重构和现代化


首先让Claude给出Plan
Prompt: `根据@CLAUDE.md，给出你关于实现该项目的Plans`



```