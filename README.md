# vs-wsl-fortran

A Fortran example project using Visual Studio and Windows Subsystem for Linux (WSL).

## Getting started

### Requirements

- Visual Studio 2019
- Windows Subsystem for Linux (WSL)

Note: This was tested on a system with Windows 10 2004, Visual Studio 16.6 and WSL 2.

### Prepare the WSL

Download and install a Linux distribution for WSL.
This example was tested with Debian Buster, but other distributions should work just as well.

Install the packages needed for your WSL installation to work with Visual Studio:
```
sudo apt install g++ gdb make ninja-build rsync zip
```
For more detailed instructions see the
[Linux development with C++](https://docs.microsoft.com/cpp/linux/download-install-and-setup-the-linux-development-workload) documentation.

In addition we need to install the `gfortran` compiler:
```
sudo apt install gfortran
```

### Build the project

Start Visual Studio and open the *vs-wsl-fortran* folder.
Select the *WSL-GCC-Debug* target, then build it.

### Run the Linux executable inside Visual Studio

Select *vs-wsl-fortran (src\vs-wsl-fortran)* as the startup item and start it (F5).
To see the output you might need to open the *Linux Console Window* view.

## Cross-compile a Windows executable

The mingw compiler can be used to create Windows binaries.
On Debian you have to install
```
sudo aptitude install gfortran-mingw-w64-x86-64
```

### Build the project for Windows

Select the *WSL-MINGW-Release* target and build it.

After building the executable you still need to copy some DLLs into that folder.
In the case of Debian these DLLs are provided by the mingw package:
```sh
cd <vs-wsl-fortran_folder>/out/build/WSL-MINGW-Release/src
cp /usr/lib/gcc/x86_64-w64-mingw32/8.3-win32/*.dll .
```

Now you can run the executable in a Windows PowerShell or CMD:
```psh
.\vs-wsl-fortran.exe
```

## Notes

### CMakeSettings.json

Ninja is not yet supported for Fortran, so *generator* has to be set to "Unix Makefiles" instead.

When cross compiling the compiler has to be specified with "-DCMAKE_Fortran_COMPILER=/usr/bin/x86_64-w64-mingw32-gfortran" in the CMake Command Arguments.
This is not necessary when targeting Linux, in that case the default `gfortran` compiler is detected automatically.

### Fortran syntax highlighting in Visual Studio

By default Visual Studio does not provide any syntax highlighting for Fortran code,
but it can be added as described [here](https://docs.microsoft.com/visualstudio/ide/adding-visual-studio-editor-support-for-other-languages).

First create the following folder:
```
%userprofile%\.vs\Extensions\Syntaxes\
```

Then download an appropriate *grammar.json* file for Fortran and store it in this folder.
You can take for example the grammar files used by the [Modern Fortran](https://github.com/krvajal/vscode-fortran-support) plugin for VSCode,
you just have to copy the .json files from

> https://github.com/krvajal/vscode-fortran-support/tree/master/syntaxes

into your Syntaxes folder.

You may need to restart Visual Studio before the new highlighting becomes visible.
