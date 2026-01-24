**Warning: This version is no longer maintained. No guarantees are made regarding the absence of issues or security vulnerabilities.**

### Supported Platforms

| Executable Group | Windows | Linux |
| :--- | :--- | :--- |
| Backend | Supported | Code exists, but lacks extensive testing and is not a maintained version. Not provided. |
| Frontend | Supported | Not Supported |

## Step 1: Download

Download the binary files from Release v6.36.109. Please ensure the downloaded executable files match your platform.

Extract `backend.rar` into one folder and `frontend.rar` into another folder.

## Step 2: Backend Configuration

The original structure after extracting the backend archive is as follows:

```
│  account.ini
│  basic_setting.ini
│  CBCOJ_Server.exe
│  loge.txt
│  logi.txt
│  logw.txt
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

`account.ini` follows this format:
*   First line: Number of accounts (an integer $n$).
*   Next $n$ lines: Each line stores information for one account, containing the username and password, separated by a space.
*   Compared to the previous version, you no longer need to manually configure user IDs. User IDs are assigned sequentially starting from $1$ according to the configuration order.

`basic_setting.ini` follows this format:
*   First line: Number of judging threads (an integer $n$).
*   Second line: Path to the folder storing source code awaiting judgment.
*   Next $n$ lines: The working folder path for each judging thread (the number of lines matches the number of judging threads).
*   Next line: Path to the Problem Base folder.
*   Next line: Path to the g++ compiler.
*   Next line: Path to the folder storing all judging results.
*   Next line: Login service port number, an integer.
*   Next line: Submission service port number, an integer.
*   Next line: Query service port number, an integer.

`logi.txt`, `loge.txt`, and `logw.txt` are log files generated when `CBCOJ_Server.exe` runs. They can be safely deleted when `CBCOJ_Server.exe` is not running.

`rc.txt` is the file storing submission IDs. Do not delete or modify this file directly!

`pb/setting.ini` stores problem configurations, where `pb` is the Problem Base folder configured in `basic_setting.ini`. Its format is as follows:
*   First line: Number of problems (an integer $n$).
*   Next $n$ lines: Each line contains a problem name.

The configuration for each problem must be saved in a subfolder under the `pb` folder. The name of this subfolder must match the problem name configured in `pb/setting.ini`.

All test data should be placed inside this problem folder. If Special Judge (SPJ) is required, place the SPJ executable file in this directory as well. The format of `setting.txt` is as follows:
*   First line: Contains the input/output file name (without extension, corresponding files are `*.in/out`, but the program should not read or write files; the judge will redirect input/output streams), the SPJ executable file name, and the number of subtasks $n$, separated by spaces.
    *   If SPJ is not needed, use `fc` instead of the executable file name.
*   Next, there are $n$ sets of subtask configuration items, following this format:
    *   The first line inputs two integers $m, k$, representing the number of test points in this subtask and the score for passing it. Then input an integer $x$ and $x$ integers $a_i$, indicating that the current subtask depends on subtasks $a_i$. $a_i$ must be **less than** the current subtask's number. Subtasks are numbered starting from $0$. All numbers are separated by spaces.
    *   Next $m$ lines, each line contains the test point file name (without extension, corresponding input/output files are stored as *.in/out), time limit (ms), and memory limit (MiB), separated by spaces.

At this point, the backend configuration is complete.

## Step 3: Frontend Configuration

The original structure after extracting the frontend archive is as follows:

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

Where `...` indicates the omission of some files not directly relevant.

`config.json` follows this format:
*   `port` (number): Port number for the user website.
*   `adport` (number): Port number for the administrator website.
*   `adaccount` (array): List of accounts used to log in to the administrator website.
*   Each element in the `adaccount` array should be an object of the form `{"username":"", "password":""}`, representing a username-password pair.
    *   `username` (string): The account's username.
    *   `password` (string): The account's password.
*   `judgeServers` (array): List of backend judging servers used for evaluation.
*   Each element in the `judgeServers` array should be an object of the form `{"id":"", "name":"", "ip":"", "loginPort":num, "judgePort":num, "queryPort":num}`, representing a backend configuration group.
    *   `id` (string): The ID of this backend configuration group. It should be a decimal string of an integer in the range $[0,255]$, without leading zeros.
    *   `ip` (string): The IPv4 address of the judging server for this configuration group.
    *   `loginPort` (number): The login service port number for this configuration group's judging server.
    *   `judgePort` (number): The submission service port number for this configuration group's judging server.
    *   `queryPort` (number): The query service port number for this configuration group's judging server.

In the `public/files` folder, you can store any files you wish users to access via the URL `yourwebsite/files/filename`. However, the default configuration does not allow access. You need to manually visit the admin webpage and change the configuration to remove `files` from the list of restricted folders.

In the `public/problem` folder, you can configure the description pages for problems. The name of the HTML file (without the extension) must be the same as the problem name.

At this point, the frontend configuration is complete.

## Step 4: Start the Services

First, start the backend (`CBCOJ_Server.exe`), then start the frontend (`server.exe`).

The website will be available at `localhost:port`, where "port" is the "port" value configured in the frontend's `config.json`.

## System Features

Login, view problems, submit code, and get judging results.

**Login**: Please visit the `yourwebsite/login` page and fill in your username and password as prompted.

(Login interface screenshot: https://github.com/chenyichen0420/CBCOJ_Releases/blob/main/statics/Login-paswd.png )

(Login success screenshot: https://github.com/chenyichen0420/CBCOJ_Releases/blob/main/statics/Login-success.png )

**View Problem List**: Visit the `yourwebsite/problem?page=...` page to get the problem list.

(Problem list screenshot: https://github.com/chenyichen0420/CBCOJ_Releases/blob/main/statics/Problemlist.png )

**View Problem Details**: Click on any problem in the problem list to view its detailed description.

(Problem details page screenshot: https://github.com/chenyichen0420/CBCOJ_Releases/blob/main/statics/Viewproblem.png )

**Submit Code**: If you have a solution for a problem, you can click the submit button below the problem and fill in your code and select the language as prompted.

(Submission interface screenshot: https://github.com/chenyichen0420/CBCOJ_Releases/blob/main/statics/Submit-code.png )

**View Results**: After clicking the submit button, please wait for judging. Once judging is complete, the webpage will automatically jump to the results page.

(Judging result screenshot: https://github.com/chenyichen0420/CBCOJ_Releases/blob/main/statics/Result_v5.png )

### Note

In fact, the provided archives contain a pre-configured environment that can be used directly. All the screenshots above are from the effects of running the default configured environment.

The screenshot of the submission interface contains the correct solution code for that problem.

### About SPJ Support in CBCOJ

CBCOJ does not support `testlib.h`, which may seem unusual and potentially inconvenient, but there are design considerations. The system will call your SPJ executable via the command line in the format: `spj.exe input_file_path user_output_file_path answer_file_path`.

Here is the SPJ sample program for problem `aplusb` (i.e., the content of `spj.cpp` in the backend archive):

```cpp
#include<bits/stdc++.h>
using namespace std;
int main(int argc, char** argv){
    ifstream in(argv[1]);
    ifstream out(argv[2]);
    ifstream ans(argv[3]);
    int av, ov;
    ans >> av;
    out >> ov;
    if(ov == av * 2) return 0;
    return 1;
}
```

If your SPJ program determines the user's output is correct, please return 0 (since runtime errors typically do not return 0, this can indicate issues like wrong output format).

### A Mysterious Bug

Occasionally, if your frontend and backend are on the same computer and you use `127.0.0.1` as the judging server's IPv4 address in `config.json`, you may be able to log in and update problems normally, but fail to get judging results.

This issue has only occurred on Win11 and has not been stably reproducible. However, a feasible workaround is to replace the judging server's IPv4 address with the computer's local network IPv4 address.
