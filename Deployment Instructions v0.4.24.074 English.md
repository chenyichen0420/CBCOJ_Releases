**Warning: This version has been discontinued and is not guaranteed to be free of issues or security vulnerabilities.**

### Supported Platforms

| Executable Group | Windows | Linux |
| :--- | :--- | :--- |
| Backend | Supported | Not Supported |
| Frontend | Supported | Not Supported |

## Step 1: Download

Download the binary files from Release v4.24.074. Ensure the downloaded executable files match the corresponding platform.

Extract `backend.rar` into one folder and `frontend.rar` into another folder.

## Step 2: Backend Configuration

The structure after extracting the backend archive is as follows:

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

`account.ini` follows this format:
*   First line: Number of accounts (an integer $n$).
*   Next $n$ lines: Each line stores information for one account: username, password, and user ID, separated by spaces.

`basic_setting.ini` follows this format:
*   First line: Number of judging threads (an integer $n$).
*   Second line: Path to the folder storing source code to be judged.
*   Next $n$ lines: Working folder path for each judging thread (the number of lines matches the number of judging threads).
*   Next line: Path to the Problem Base folder.
*   Next line: Path to the folder storing all judging results.
*   Next line: Path to the g++ compiler.

`log.txt` is the log file generated when `CBCOJ_Server.exe` runs. It can be safely deleted when `CBCOJ_Server.exe` is not running.

`rc.txt` is the file storing submission IDs. Do not directly delete or modify this file!

`pb/setting.ini` stores problem configurations, where `pb` is the Problem Base folder configured in `basic_setting.ini`. Its format is as follows:
*   First line: Number of problems (an integer $n$).
*   Next $n$ lines: Each line contains the name of one problem.

The configuration for each problem must be saved in a subfolder under the `pb` folder. The subfolder's name must match the problem name configured in `pb/setting.ini`.

All test data should be placed in this problem folder. If special judge (SPJ) is needed, please place the SPJ executable file in this directory as well. The format of `setting.txt` is as follows:
*   First line: Contains the number of test cases, input/output filenames (without extensions, corresponding input/output files are `*.in/out`, i.e., the program should open `*.in` to read input and output to `*.out`), and the executable filename needed for SPJ, separated by spaces.
    *   If SPJ is not needed, use `fc` instead of the executable filename.
*   Subsequent lines: Configuration for each test case, including input/output filenames (without extensions, corresponding input/output files are stored as `*.in/out`), time limit (ms), and memory limit (MiB).

At this point, backend configuration is complete.

## Step 3: Frontend Configuration

The structure after extracting the frontend archive is as follows:

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

Here, `...` indicates that some files not directly relevant have been omitted.

`config.json` follows this format:
*   `port` (number): The port number for the user website.
*   `adport` (number): The port number for the administrator website.
*   `ip` (string): The IPv4 address of the judging machine (backend).
*   `adaccount` (array): A list of accounts for logging into the administrator website.
*   Each element in the `adaccount` array should be an object of the form `{"username":"", "password":""}`, representing a username and password pair.
    *   `username` (string): The account's username.
    *   `password` (string): The account's password.

In the `public/files` folder, you can store any files you wish users to access. They can be accessed via the URL `yourwebsite/files/filename`.

In the `public/problem` folder, you can configure problem description pages. The name of the HTML file (without extension) must be the same as the problem name.

At this point, frontend configuration is complete.

## Step 4: Start Services

First, start the backend (`CBCOJ_Server.exe`), then start the frontend (`server.exe`).

The website will be available at `localhost:port`, where "port" is the "port" value configured in the frontend's `config.json`.

## System Features

Logging in, viewing problems, submitting code, and obtaining judging results.

**Login**: Please visit the `yourwebsite/login` page and fill in your username and password as prompted to log in.

(Login interface screenshot: https://github.com/chenyichen0420/CBCOJ_Releases/blob/main/statics/Login-paswd.png )

(Login success screenshot: https://github.com/chenyichen0420/CBCOJ_Releases/blob/main/statics/Login-success.png )

**View Problem List**: Access the `yourwebsite/problem?page=...` page to get the problem list.

(Problem list screenshot: https://github.com/chenyichen0420/CBCOJ_Releases/blob/main/statics/Problemlist.png )

**View Problem Details**: Click on any problem in the problem list to view its detailed description.

(Problem details page screenshot: https://github.com/chenyichen0420/CBCOJ_Releases/blob/main/statics/Viewproblem.png )

**Submit Code**: If you have a solution for a problem, you can click the submit button below the problem and follow the prompts to fill in your code and select the language.

(Submission interface screenshot: https://github.com/chenyichen0420/CBCOJ_Releases/blob/main/statics/Submit-code.png )

**View Results**: After clicking the submit button, please wait for the judging. Once judging is complete, the webpage will automatically jump to the results page.

(Judging result screenshot: https://github.com/chenyichen0420/CBCOJ_Releases/blob/main/statics/Result.png )

### Note

In fact, the provided archives contain a pre-configured environment that can be used directly. All the above screenshots are from the effects of running the default configured environment.

The screenshot of the submission interface contains the correct solution code for that problem.

### About CBCOJ's SPJ Support

CBCOJ does not support `testlib.h`, which may seem unusual and potentially inconvenient, but there are design considerations. The system will call your SPJ executable via command line in the format: `spj.exe input_file_path answer_file_path user_output_file_path`.

The following is the SPJ example program for problem `aplusb` (i.e., the content of `spj.cpp` in the backend archive):

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

If your SPJ program determines the user's output is correct, please return 0 (since runtime errors typically do not return 0, this can indicate issues like incorrect output format).
