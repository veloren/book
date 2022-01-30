# Debugging

This section covers some helpful debugging tips within the Veloren project. This should help if you wish to explore the code base at runtime, or work on implementing a feature.

# Compiling With Debug Symbols

In order for debug symbols to be generated for the project, the `debuginfo` profile must be used. You can build the project with debug symbols included by running this command:

```bash
cargo build -Z unstable-options --profile debuginfo
```

# Visual Studio Code

Follow [this guide](https://www.forrestthewoods.com/blog/how-to-debug-rust-with-visual-studio-code/) to setup your vscode installation.

After that make the following modifcations to `launch.json` (remember to build with the `cargo` command listed above!)

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "(Windows) Launch",
      "type": "cppvsdbg",
      "request": "launch",
      "program": "${workspaceRoot}\\target\\debuginfo\\veloren-voxygen.exe",
      "args": [],
      "stopAtEntry": false,
      "cwd": "${workspaceRoot}",
      "environment": [],
      "externalConsole": true
    },
    {
      "name": "(OSX) Launch",
      "type": "lldb",
      "request": "launch",
      "program": "${workspaceRoot}/target/debuginfo/veloren-voxygen",
      "args": [],
      "cwd": "${workspaceRoot}"
    }
  ]
}
```

# Jetbrains Integrated Development Environments
Please do note that debugging on Jetbrains IDEs is only supported on a small subset of their products (like CLion or IntelliJ Idea Ultimate). Visit [this link](https://github.com/intellij-rust/intellij-rust) for further information.

Install [This plugin](https://github.com/intellij-rust/intellij-rust) in your IDE (either via File -> Settings -> Plugins [Ctrl + Alt + x], or via your browser) and open your rust project in the IDE.

Click the button "Add Configuration..." in the upper right corner. This will open a window giving you the ability to create launch / debug profiles.

Click the little "+" button and select "Cargo in the dropdown". This will create you a launch profile.

Edit the "Name" field however you want. Then here's the interesting part : Editing the "Command" field 

By default, the "Command" field should have "run" in it, keep it and add "--bin {bin} --profile debuginfo -Z unstable-options" where bin is the name of the binary to debug (veloren-server-cli, veloren-voxygen, ...).

The "Command" field should then contain something similar to "run --bin veloren-server-cli --profile=debuginfo -Z unstable-options".

If you have any question, please reach out to me (infrandomness#4003) on the Veloren discord server :P.

## Troubleshooting

Note: Some users have reported needing to run VSCode as an administrator for debugging to work correctly.
If you notice an error message similar to below, then try re-running VSCode as administrator.

```
Unable to open 'panicking.rs': Unable to read file (Error: File not found
(c:\rustc\7dbfb0a8ca4ab74ee3111e57a024f9e6257ce37c\src\libstd\panicking.rs)).
```
