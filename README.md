## Mac 配置

参考：https://code.visualstudio.com/docs/cpp/config-clang-mac

### 编译配置：

#### tasks.json

~~~json
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
      {
        "type": "shell",
        "label": "clang++ build active file",
        "command": "/usr/bin/clang++",
        "args": [
          "-std=c++17",
          "-stdlib=libc++",
          "-g",
          "${file}",
          "-o",
          "${fileDirname}/build/${fileBasenameNoExtension}"
        ],
        "options": {
          "cwd": "${workspaceFolder}"
        },
        "problemMatcher": ["$gcc"],
        "group": {
          "kind": "build",
          "isDefault": true
        }
      }
    ]
}
~~~  


#### 编译

选择要编译的文件（必须），然后敲 `Command+Shift+B`或选菜单项：`Terminal > Run Build Task`

#### 执行：

~~~bash
$ build//helloworld
~~~

### Debug 配置

#### launch.json

~~~json
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "clang++ - Build and debug active file",
      "type": "cppdbg",
      "request": "launch",
      "program": "${fileDirname}/build/${fileBasenameNoExtension}",
      "args": [],
      "stopAtEntry": true,
      "cwd": "${workspaceFolder}",
      "environment": [],
      "externalConsole": false,
      "MIMode": "lldb",
      "preLaunchTask": "clang++ build active file"
    }
  ]
}
~~~

#### 执行调试

回到源代码按 F5 或在 Debug tab 下选择 RUN AND DEBUG: "clang++ - Build and debug active file"


### C/C++ configuration

更多的 c/c++ 配置，比如选择 c++ 标准的版本号等，有两种方法：

按 `command+shift+P`: 输入 `C/C++: Edit Configurations (UI)` 打开 UI 界面，或者需要用到 c_cpp_properties.json 配置文件：

#### c_cpp_properties.json

~~~json
{
    "configurations": [
        {
            "name": "Mac",
            "includePath": [
                "${workspaceFolder}/**"
            ],
            "defines": [],
            "macFrameworkPath": [
                "/System/Library/Frameworks",
                "/Library/Frameworks"
            ],
            "compilerPath": "/usr/bin/clang",
            "cStandard": "c11",
            "cppStandard": "c++17",
            "intelliSenseMode": "clang-x64"
        }
    ],
    "version": 4
}
~~~

