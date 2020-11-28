# Reporting Bugs

1. First thing to do will be to check our [gitlab issues](https://gitlab.com/veloren/veloren/issues) if this bug is already known.
2. If not [create an issue](https://gitlab.com/veloren/veloren/issues/new?issue%5Bassignee_id%5D=&issue%5Bmilestone_id%5D=) with the `Bug template` and try to describe the bug as good as possible, include screenshots if needed.
3. Upload the log file for additional information which can help us identify the issue. See below how to get logs.
   (**Note:** make sure no sensitive information is included in the log files)
4. Submit the issue

**Tip**: _Incase you do not want to create an gitlab account you can join our [discord](https://discord.gg/BvQuGze)
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