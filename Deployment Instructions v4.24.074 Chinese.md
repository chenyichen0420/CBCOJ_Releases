**警告：此版本已停止维护，不保证不存在问题或安全漏洞。**

### 支持的平台

| 可执行文件组 | Windows | Linux |
| :--- | :--- | :--- |
| 后端 | 支持 | 不支持 |
| 前端 | 支持 | 不支持 |

## 第一步：下载

从 Release v4.24.074 下载二进制文件。请确保下载的可执行文件与对应平台匹配。

将 `backend.rar` 解压到一个文件夹，将 `frontend.rar` 解压到另一个文件夹。

## 第二步：后端配置

后端压缩包解压后的原始结构如下：

```
│  account.ini
│  basic_setting.ini
│  CBCOJ_Server.exe
│  log.txt
│  rc.txt
│
├─rec
├─work
├─work1
├─work2
└─pb
   │  setting.ini
   │
   └─aplusb
           setting.txt
           spj.cpp
           spj.exe
           test1.in
           test1.out
           test2.in
           test2.out
```

`account.ini` 遵循以下设置格式：
*   第一行：账户数量（一个整数 $n$）。
*   后续 $n$ 行：每行存储一个账户的信息，依次为用户名、密码和用户ID，以空格分隔。

`basic_setting.ini` 遵循以下设置格式：
*   第一行：评测线程数（一个整数 $n$）。
*   第二行：存放待评测源代码的文件夹路径。
*   接下来 $n$ 行：每个评测线程的工作文件夹路径（行数与评测线程数一致）。
*   下一行：题目库（Problem Base）的文件夹路径。
*   下一行：存放所有评测结果的文件夹路径。
*   下一行：g++ 编译器的路径。

`log.txt` 是 `CBCOJ_Server.exe` 运行时生成的日志文件。在 `CBCOJ_Server.exe` 未运行时可以安全删除。

`rc.txt` 是存储提交ID的文件。请勿直接删除或修改此文件！

`pb/setting.ini` 存储题目的配置，其中 `pb` 是在 `basic_setting.ini` 中配置的题目库文件夹。其格式如下：
*   第一行：题目数量（一个整数 $n$）。
*   后续 $n$ 行：每行一个题目的名称。

每个题目的配置必须保存在 `pb` 文件夹下的一个子文件夹中，该子文件夹的名称需与 `pb/setting.ini` 中配置的题目名称一致。

所有测试数据都应放在此题目文件夹内。如果需要特殊评测（SPJ），请将SPJ所需的可执行文件也放在此目录下。`setting.txt` 的格式如下：
*   第一行：包含测试用例数量、输入/输出文件名（不包含扩展名，对应的输入输出文件为 `*.in/out`，即程序应当打开 `*.in` 读取输入并输出到 `*.out`）以及 SPJ 所需的可执行文件名，以空格分隔。
    *   如果不需要SPJ，请用 `fc` 代替可执行文件名。
*   后续行：每个测试用例的配置，包括输入/输出文件名（不包含扩展名，对应的输入输出文件存储为为 `*.in/out`）、时间限制（ms）和内存限制（MiB）。

至此，后端配置完成。

## 第三步：前端配置

前端压缩包解压后的原始结构如下：

```
│  config.json
│  server.exe
│
├─admin
│  │  ...
│  │
│  └─assets
│          ...
│
└─public
    │  ...
    │
    ├─api
    ├─files
    ├─login
    │      ...
    │
    ├─problem
    │      aplusb.html
    │
    ├─records
    ├─submit
    │      ...
    │
    └─templates
       ...
```

其中 `...` 表示省略了一些不直接相关的文件。

`config.json` 遵循以下设置格式：
*   `port`（数字）：用户网站的端口号。
*   `adport`（数字）：管理员网站的端口号。
*   `ip`（字符串）：评测机（后端）的IPv4地址。
*   `adaccount`（数组）：用于登录管理员网站的账户列表。
*   `adaccount` 数组中的每个元素应为 `{"username":"", "password":""}` 形式的对象，代表一对用户名和密码。
    *   `username`（字符串）：账户的用户名。
    *   `password`（字符串）：账户的密码。

在 `public/files` 文件夹中，您可以存放任何希望用户访问的文件，通过网址 `yourwebsite/files/文件名` 即可访问。

在 `public/problem` 文件夹中，您可以配置题目的描述页面。HTML文件的名称（不含扩展名）必须与题目名称相同。

至此，前端配置完成。

## 第四步：启动服务

首先启动后端（`CBCOJ_Server.exe`），然后启动前端（`server.exe`）。

网站将在 `localhost:port` 上可用，其中“port”是前端 `config.json` 中配置的“port”值。

## 系统功能

登录、查看题目、提交代码、获取评测结果。

**登录**：请访问 `yourwebsite/login` 页面，根据提示填写用户名和密码即可登录。
（登录界面示意图：https://github.com/chenyichen0420/CBCOJ_Releases/blob/main/statics/Login-paswd.png）
（登录成功示意图：https://github.com/chenyichen0420/CBCOJ_Releases/blob/main/statics/Login-success.png）

**查看题目列表**：访问 `yourwebsite/problem?page=...` 页面可以获取题目列表。
（题目列表示意图：https://github.com/chenyichen0420/CBCOJ_Releases/blob/main/statics/Problemlist.png）

**查看题目详情**：点击题目列表中的任一题目，即可查看该题目的详细描述。
（题目详情页示意图：https://github.com/chenyichen0420/CBCOJ_Releases/blob/main/statics/Viewproblem.png）

**提交代码**：如果您对某题有了解决方案，可以点击题目下方的提交按钮，并根据提示填写代码和选择语言。
（提交界面示意图：https://github.com/chenyichen0420/CBCOJ_Releases/blob/main/statics/Submit-code.png）

**查看结果**：点击提交按钮后，请等待评测。评测完成后，网页将自动跳转到结果页面。
（评测结果示意图：https://github.com/chenyichen0420/CBCOJ_Releases/blob/main/statics/Result.png）

### 附注

实际上，提供的压缩包内包含一个已配置好的、可直接使用的环境。以上所有截图均来自运行默认配置环境的效果。

提交界面的截图中包含了该题目的正确解答代码。

### 关于 CBCOJ 的 SPJ 支持

CBCOJ 不支持 `testlib.h`，这看起来有些特别且可能不够便利，但有其设计考量。系统会通过命令行调用您的SPJ可执行文件，格式为：`spj.exe 输入文件路径 答案文件路径 用户输出文件路径`。

以下是题目 `aplusb` 的SPJ示例程序（即后端压缩包中 `spj.cpp` 的内容）：

```cpp
#include<bits/stdc++.h>
using namespace std;
int main(int argc, char** argv){
    ifstream in(argv[1]);
    ifstream ans(argv[2]);
    ifstream out(argv[3]);
    int av, ov;
    ans >> av;
    out >> ov;
    if(ov == av * 2) return 0;
    return 1;
}
```

如果您的SPJ程序判定用户输出正确，请返回 0（因为运行时错误通常不会返回 0，这可以表明用户输出格式错误等问题）。
