---
layout: post
title: how-i-use-claude-code
date: 2025-10-20 18:43 +0800
---


怎么配置CLAUDE.md

可以在CLAUDE.md加入很多Rules，Markdown，用标题作为

个人部分：代码风格
举例说明：
- 如：遵循PEP 585 PEP 604，字符串优先使用双引号，等，纯属个人偏好
> # Python Code Styles
> - Python PEP 585
>  As of Python 3.9, the use of typing.List and typing.Dict is deprecated in favor of the built-in types `list` and `dict`.
> - Python PEP 604
>  In Python 3.10 and later, you can use the | operator to define union types directly in type hints, eliminating the need to import Union or use Optional.
> - Usage of quotes
>   Prefer double quotes (") over single quotes (') for defining strings.
> - Always run `python` using `uv`, i.e., `uv run python ...`


几种场景
```text
project-name/
│
├── src/                          # 核心功能（推荐使用具体名称，your_application）
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

- 开始全新项目
  放入代码风格、项目结构
  - 首先自己给feature模块命名：src/feature_a.py，写好基本框架：函数&出入参数，以及#TODOs
  - prompt：实现@src/feature_a.py里的所有#TODO
  - 然后开始测试脚本（尽量不要在src/里加入测试脚本）
  - prompt: 帮助我实现一个测试@src/feature_a.py功能的脚本，复制@tests/template.py，/tests/test_feature_a.py，要求验证<某某功能>，不要使用Mock数据！#TODO: improve this prompt

- 对于接近开发完成项目的bug修复
fix bug

- 拿到开源项目/别人开发完项目如何快速上手


项目结构
project-name
--> /src or /your_application  具体feature代码，尽量不要出现测试代码
--> /tests  测试代码
------> context.py
------> template.py content: import context\n"""Do not insert any code above!!!"""\n
--> /docs  文档：针对比较复杂feature的说明/接口调用说明

coding pipeline
自己给feature模块命名，写好框架以及TOOD

帮写测试脚本

功能代码放到/src 或者 /your_application，测试模块放/tests，context.py，文档放/docs

比如完成了一个功能feature_a.py，
然后写测试文件的prompt: 帮助我实现一个测试@src/feature_a.py功能的脚本，复制@tests/template.py，/tests/test_feature_a.py，要求验证<某某功能>，不要使用Mock数据！#TODO: improve this prompt



帮助使用git add以及git commit（介绍一下claude-code会运行的指令）

2 定义一些常用的脚本：举例，统计每日/每周AI协助代码

如何

3 工具的使用

MCP

4 权限
默认是没有写权限，以及除了ls其他指令的权限，所有的权限需要人介入赋予权限
`claude --dangerously-skip-permissions`直接赋予权限（不建议）

推荐只给基础权限

5 AI generated code review


参考
https://www.anthropic.com/engineering/claude-code-best-practices