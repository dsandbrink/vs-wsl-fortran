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
For more detailed instructions see https://docs.microsoft.com/cpp/linux/download-install-and-setup-the-linux-development-workload.

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
