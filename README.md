# RyzenAdj
Adjust power management settings for Ryzen Processors.

[![Build Status](https://travis-ci.org/FlyGoat/RyzenAdj.svg?branch=master)](https://travis-ci.org/FlyGoat/RyzenAdj)

Based on: [FlyGoat/ryzen_nb_smu](https://github.com/flygoat/ryzen_nb_smu)

RyzenAdjUI_WPF by "JustSkill" is no longer maintained, for GUI please see [le.storm1er/ryzen-controller](https://gitlab.com/le.storm1er/ryzen-controller).

## Usage
The command line interface is identical on both Windows and Unix-Like OS.

You should run it with Administrator on Windows or root on Linux.

You can write a shell script or bat to do it automaticly.

```
$./ryzenadj -h
Usage: ryzenadj [options] [[--] args]
   or: ryzenadj [options]

 Ryzen Power Management adjust tool.

    -h, --help                            show this help message and exit

Options
    -i, --info                            Show information (W.I.P.)

Settings
    -a, --stapm-limit=<u32>               Sustained Power Limit         - STAPM LIMIT (mW)
    -b, --fast-limit=<u32>                Actual Power Limit            - PPT LIMIT FAST (mW)
    -c, --slow-limit=<u32>                Average Power Limit           - PPT LIMIT SLOW (mW)
    -d, --slow-time=<u32>                 Slow PPT Constant Time (s)
    -e, --stapm-time=<u32>                STAPM constant time (s)
    -f, --tctl-temp=<u32>                 Tctl Temperature Limit (degree C)
    -g, --vrm-current=<u32>               VRM Current Limit             - TDC LIMIT VDD (mA)
    -j, --vrmsoc-current=<u32>            VRM SoC Current Limit         - TDC LIMIT SoC (mA)
    -k, --vrmmax-current=<u32>            VRM Maximum Current Limit     - EDC LIMIT VDD (mA)
    -l, --vrmsocmax-current=<u32>         VRM SoC Maximum Current Limit - EDC LIMIT SoC (mA)
    -m, --psi0-current=<u32>              PSI0 VDD Current Limit (mA)
    -n, --psi0soc-current=<u32>           PSI0 SoC Current Limit (mA)
    -o, --max-socclk-frequency=<u32>      Maximum SoC Clock Frequency (MHz)
    -p, --min-socclk-frequency=<u32>      Minimum SoC Clock Frequency (MHz)
    -q, --max-fclk-frequency=<u32>        Maximum Transmission (CPU-GPU) Frequency (MHz)
    -r, --min-fclk-frequency=<u32>        Minimum Transmission (CPU-GPU) Frequency (MHz)
    -s, --max-vcn=<u32>                   Maximum Video Core Next (VCE - Video Coding Engine) (Value)
    -t, --min-vcn=<u32>                   Minimum Video Core Next (VCE - Video Coding Engine) (Value)
    -u, --max-lclk=<u32>                  Maximum Data Launch Clock (Value)
    -v, --min-lclk=<u32>                  Minimum Data Launch Clock (Value)
    -w, --max-gfxclk=<u32>                Maximum GFX Clock (Value)
    -x, --min-gfxclk=<u32>                Minimum GFX Clock (Value)
    -y, --prochot-deassertion-ramp=<u32>  Ramp Time After Prochot is Deasserted (Value): limit power based on value, higher values does apply tighter limits after prochot is over
    --apu-skin-temp=<u32>                 APU Skin Temperature Limit    - STT LIMIT APU (degree C)
    --dgpu-skin-temp=<u32>                dGPU Skin Temperature Limit   - STT LIMIT dGPU (degree C)
    --apu-slow-limit=<u32>                APU PPT Slow Power limit for A+A dGPU platform - PPT LIMIT APU (mW)
``` 

### Demo
If I'm going to set all the Power Limit to 45W, and Tctl to 90 °C,
then the command line should be:
```
./ryzenadj --stapm-limit=45000 --fast-limit=45000 --slow-limit=45000 --tctl-temp=90
```

### Documentation

- [Renoir Tuning Guide](https://github.com/FlyGoat/RyzenAdj/wiki/Renoir-Tuning-Guide)
- [FAQ](https://github.com/FlyGoat/RyzenAdj/wiki/FAQ)

## Build

### Build Requirements

Building this tool requires C & C++ compilers as well as **cmake**. It
requires privileged access to NB PCI config space, in order to compile it
one must have pcilib library & headers available.

### Linux

Please make sure that you have libpci dependency before compiling. On
Debian-based distros this is covered by installing **pcilib-dev** package:

    sudo apt install libpci-dev

On Fedora:
```
sudo dnf install pciutils-devel
```

The simplest way to build it:

    mkdir build && cd build
    cmake ..
    make

### Windows

It can be built by Visual Studio + MSVC automaticaly, or Clang + Nmake in command line.
However, as for now, MingW-gcc can't be used to compile for some reason.

Required dll is included in ./prebuilt of source tree. Please put the dll
library and sys driver in the same folder with ryzenadj.exe.

We don't recommend you to build by yourself on Windows since the environment configuarion
is very complicated. If you would like to use ryzenadj functions in your program, see libryzenadj.
