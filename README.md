ECO32 on macOS
=================

Welcome!

This small project extends the both projects ECO32 [1] and
EOS32 on ECO32 [2] and allows it to compile and run the 
ECO32 simulator together with the EOS32 operating system 
natively on macOS under Apple Silicon!

[1] https://github.com/hgeisse/eco32

[2] https://github.com/hgeisse/eos32-on-eco32

Prerequisites
-------------
Under macOS you need some additional software to compile
both projects. Most of this software can be installed with
the Homebrew package management system [3].

On a fresh installation of macOS you have to follow these steps:

1. Install XCode command line tools by running
    `xcode-select --install`.
2. Install `util-linux`, e.g. via Homebrew (`brew install util-linux`). This package contains _libuuid_, which is a requirement for the GPT part of the system.
3. Install `byacc`, e.g. via Homebrew (`brew install byacc`). The _yacc_ shipped with the XCode tools won't work properly with our source code. After installing you have to create a proper symbolic link from _yacc_ to _byacc_ with `ln -s /opt/homebrew/bin/byacc /opt/homebrew/bin/yacc` (paths may vary).
4. Install _XQuartz_, e.g. via Homebrew (`brew install --cask xquartz`). This is a X server for macOS.

[3] https://brew.sh/

Compile the project
-------------------
Small changes to the source code are needed to compile both projects under macOS. You can apply these changes with the shipped _patch_ files. The following shell commands basically just clone the according repositories and apply the mentioned patches.

```
# clone this repository
git clone https://github.com/swlt16/eco32-on-mac
cd eco32-on-mac

# clone original repositories (use fp branch of eco32!)
git clone https://github.com/hgeisse/eco32 -b fp
git clone https://github.com/hgeisse/eos32-on-eco32

# apply patches
patch -p0 < eco32.patch
patch -p0 < eos32.patch
```

Afterwards you can compile and run both projects as usual. 
See the individual READMEs for further information.

Notes 
-----
Due to compatibility issues this project disables the interactive mode for the simulator by omitting the `-i` switch.

This project was tested with the following software versions:
- macOS Sequoia 15.2 on a MacBook Air M2
- ECO32 on the `fp` branch with HEAD at commit `dbca03b`
- EOS32 with HEAD at commit `ce67b96`

**IMPORTANT**: This _should_ work without problems. But I cannot promise that. So be prepared for weird issues!