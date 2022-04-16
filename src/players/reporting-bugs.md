# Reporting Bugs

1. First thing to do will be to check our [gitlab issues](https://gitlab.com/veloren/veloren/issues) if this bug is already known.
2. If not [create an issue](https://gitlab.com/veloren/veloren/issues/new?issue%5Bassignee_id%5D=&issue%5Bmilestone_id%5D=) with the `Bug template` and try to describe the bug as good as possible, include screenshots if needed.
3. Upload the log file for additional information which can help us identify the issue. See below how to get logs.
   (**Note:** make sure no sensitive information is included in the log files)
4. Submit the issue

**Tip:** _Incase you do not want to create an gitlab account you can join our [discord](https://discord.gg/BvQuGze)
and report the bug in `#bugs-and-support`._

# Collect Logs

If you encounter problems with Veloren, we might ask you for logs or a trace.
This tutorial shows you how to collect the logs, depending on your operating system, and the way you have installed Veloren.

By default Veloren server and Voxygen will both produce logs.
They are printed in the terminal/cmd and to a file, called `voxygen.log.<todays_date>`. It even prints where the file is located to terminal/cmd:
```
Nov 25 01:40:14.388  INFO veloren_voxygen::logging: Setup terminal and file logging. logdir="/mnt/games/cargo-build/debug/userdata/voxygen/logs"
```

By default the granularity is `INFO`, but please provide logs on `TRACE` level (as shown below).
Search for a message called `Tracing is successfully set to TRACE` to verify `TRACE` level is enabled.

## Linux and MacOS

#### Airshipper

1. Start airshipper with ` -vv` argument.
2. When the game starts it will print to the terminal the location of the log file.
   Check [Airshipper](airshipper.md) page.

#### Compiled

1. Start voxygen with `TRACE` level in terminal:
    ```
    RUST_LOG="trace" ./target/debug/veloren-voxygen
    # or RUST_LOG="trace" cargo run
    ```
2. Copy trace from terminal or the log file mentioned above.

## Windows

#### Airshipper

1. Opening a CMD.
   > On Windows press `Windows key + R`. Then type `cmd` and hit `enter`.
2. Type `airshipper run -vv` and hit enter.
3. Run the game (till you encounter the problem).
4. The logs should be located in `%Appdata%/airshipper/profiles/default/userdata/voxygen/logs`
   Or check [Airshipper](airshipper.md) page.
#### Compiled

##### Git Bash
-> See Linux/Compiled above

##### Cmd

1. Open a CMD.
2. Go to your veloren folder with the `cd` command, e.g. `cd C:\Users\<Your Username>\Desktop\veloren`.
3. Write `set RUST_LOG=trace&& veloren-voxygen.exe` and hit enter (exactly like here, without whitespace before `&&`)
4. The logs will now be printed to the CMD and the folder `userdata\voxygen\logs` or `%appdata%\veloren\`.

# Collecting info for graphics bugs

Sometimes it can be useful to collect extra information when debugging graphics issues. This info is not always needed so this mainly serves as a reference to point users to when the information would be helpful.

## wgpu API trace

1. Create a folder that to hold the trace. (e.g. `wgpu-trace`)
    ```shell
        mkdir wgpu-trace
    ```
2. Run the game with the envionment variable `WGPU_TRACE_DIR` set to the new folder.  
    (the path can be absolute or relative)
    #### Linux
    ```shell
        WGPU_TRACE_DIR="./wgpu-trace" airshipper start
    ```
    #### Windows
    ```shell
        set "WGPU_TRACE_DIR=./wgpu-trace"
        airshipper start
    ```
3. Reproduce the bug/crash and then exit the game (the trace will be larger if this takes a while).
4. Zip up the trace folder for easy sharing.

For more details about wgpu's API tracing see <https://github.com/gfx-rs/wgpu/wiki/Debugging-wgpu-Applications#tracing-infrastructure>

## Dx12/Dx11 debug layer output

First, check that you are using the dx12 or dx11 graphics backend.

#### Using DebugView

1. Force the debug layer on for Voxygen (Note: if you compiled the game yourself without `--release` then this step can be skipped):
    1. Run `dxcpl`.
    2. Click "edit list".
    3. Add `veloren-voxygen.exe` and click ok.
    4. Make sure "Force On" is selected in the debug layer section.
    5. Click "Apply".
2. [Download DebugView](https://docs.microsoft.com/en-us/sysinternals/downloads/debugview).
3. Start DebugView.
4. Start voxygen and run until the crash/error occurs.
5. In DebugView, File -> Save.
6. Share output file.
7. Run `dxcpl` again and remove voxygen from the list.

#### Using Visual Studio

1. Install visual studio <https://visualstudio.microsoft.com/downloads/>.
2. Force the debug layer on for Voxygen (Note: if you compiled the game yourself without `--release` then this step can be skipped):
    1. Open visual studio.
    2. Go to Debug > Graphics > Directx control panel.
    3. Click the `Edit List...` button..
    4. Add `veloren-voxygen.exe` to the list (be sure to remove this when finished).
    5. Change the Debug Layer setting to Force On.
    6. Click apply and exit the control panel.
3. Open the Voxygen executable as a project ([original instructions](https://docs.microsoft.com/en-us/visualstudio/debugger/how-to-debug-an-executable-not-part-of-a-visual-studio-solution?view=vs-2019#to-create-a-new-exe-project-for-an-existing-app)):
    1. In visual studio: File > Open > Project.
    2. Navigate to veloren-voxygen.exe, select it, and click open.
4. Run the project (green arrow and or option under the Debug menu).
5. Reproduce the issue.
6. Visual studio will have a section labeled "Output" with the output of the graphics debug layer and other random stuff (this can be shared via copy-paste).
