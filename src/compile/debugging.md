# Debugging Veloren
This section covers some helpful debugging tips within the Veloren project. This should help if you wish to explore the code base at runtime, or work on implementing a feature.

So far, debugging has been reported to be working on the following IDE configurations:
- Visual Studio Code (Windows)
- Visual Studio (Windows)

# Compiling With Debug Symbols
In order for debug symbols to be generated for the project, the `debuginfo` profile must be used. You can build the project with debug symbols included by running this command:
```
cargo build -Z unstable-options --profile debuginfo
```

# Visual Studio Code

In order to debug using VSCode, the following extensions must be installed:
```
C/C++ (Microsoft)
Rust (kalitaalexy)
Native Debug (WebFreak)
```

Once the extensions have been installed and configured, the following `launch.json` file will launch the project with debug mode enabled (remember to build with the `cargo` command listed above!)
```
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(Windows) Launch",
            "type": "cppvsdbg",
            "request": "launch",
            "program": "${workspaceFolder}\\target\\debuginfo\\veloren-voxygen.exe",
            "args": [],
            "stopAtEntry": false,
            "environment": [],
            "externalConsole": false,
            "symbolSearchPath": ""
        }
    ]
}
```

## Troubleshooting
Note: Some users have reported needing to run VSCode as an administrator for debugging to work correctly.
If you notice an error message similar to below, then try re-running VSCode as administrator.
```
Unable to open 'panicking.rs': Unable to read file (Error: File not found (c:\rustc\7dbfb0a8ca4ab74ee3111e57a024f9e6257ce37c\src\libstd\panicking.rs)).
```