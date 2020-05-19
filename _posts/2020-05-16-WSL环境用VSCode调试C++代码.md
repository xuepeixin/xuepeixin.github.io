---
layout:     post
title:      WSL环境用VSCode调试C++代码
date:       2020-05-16
author:     XPX
header-img: img/post-bg-desk.jpg
catalog: true
tags:
    - 环境配置
---

### WSL是是由微软与 Canonical 公司合作开发的 Windows 子系统，在WSL环境中，需要对VSCODE进行配置才能调试C++程序


1. 首先VSCode需要安装C/C++拓展插件
2. 选择 `调试` -> `添加配置` -> `C++(GDB/LLDB)`, 将生成的`launch.json`替换为以下内容:

```
{ 
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) Bash on Windows Launch",
            "type": "cppdbg",
            "request": "launch",
            "program": "/mnt/c/C++Projects/test/a.out(注意修改)",
            "args": [],
            "stopAtEntry": false,
            "miDebuggerArgs": "",
            "cwd": "/mnt/c/C++Projects/test/(注意修改)",
            "environment": [],
            "externalConsole": false,
            "sourceFileMap": {
                "/mnt/c/": "C:\\"
            },
            "pipeTransport": {
                "debuggerPath": "/usr/bin/gdb",
                "pipeProgram": "${env:windir}\\system32\\bash.exe",
                "pipeArgs": [
                    "-c"
                ],
                "pipeCwd": ""
            },
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ]
        },
    ]
}
```

#### 参数：

- `program` : 被调试的可执行文件.需要修改
- `sourceFileMap` : 由 wsl 到的 windows 的目录映射.如果test.c不在C盘需要修改
- `cwd` : 可执行文件的运行目录.
- `stopAtEntry` : 是否在main函数起点暂停. args : 可执行文件的参数.

### 调试

- 如果是在终端使用gcc编译：  启动终端, 输入 bash 进入wsl, 运行 gcc -g test.c , -g 选项开启调试模式.
- 如果是使用CMake进行编译，在CMakeLists.txt设置调试选项

```
SET(CMAKE_BUILD_TYPE "Debug")
SET(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g2 -ggdb")
SET(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")
```
