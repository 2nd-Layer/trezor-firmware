# Build instructions for Emulator (Unix port)

First clone, initialize submodules, install Pipenv and enter the Pipenv shell as 
defined [here](index.md). **Do not forget you need to be in a `pipenv shell`
environment!**

## Dependencies

Install the required packages, depending on your operating system.

* __Debian/Ubuntu__:

```sh
sudo apt-get install scons libsdl2-dev libsdl2-image-dev
```

* __Fedora__:

```sh
sudo yum install scons SDL2-devel SDL2_image-devel
```

* __OpenSUSE__:

```sh
sudo zypper install python3-devel python3-pip scons libSDL2-devel libSDL2_image-devel
```

* __Arch__:

```sh
sudo pacman -S scons sdl2 sdl2_image
```

* __NixOS__:

There is a `shell.nix` file in the root of the project. Just run the following **before** entering the `core` directory:

```sh
nix-shell
```

* __Mac OS X__:

```sh
brew install scons sdl2 sdl2_image pkg-config
```

* __Windows__: not supported yet, sorry.
If you're using Windows 10, you can utilize [Windows Sybsystem for Linux](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux), first [install WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10). By opening a PowerShell terminal with Administrator priviledges and running the command below; restart the system when prompted.

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

After restart of the system, visit [openSUSE Leap 15 page in Microsoft Store](https://www.microsoft.com/store/productId/9NJFZK00FGKV) and install the system by pressing **Get** button. openSUSE Leap 15 will download and installs. Once the installation is done, you can continue by installing required packages as follows:

```
sudo zypper install -y git-core python3-devel python3-pip scons libSDL2-devel libSDL2_image-devel xorg-x11
sudo pip install pipenv
```

Then clone `trezor/trezor-firmware` repository, initialize `pipenv` and build the emulator.
```
git clone https://github.com/trezor/trezor-firmware.git
cd trezor-firmware && pipenv sync
pipenv shell
cd core
make build_unix
```

Once the emulator is built properly, you also need to install Xorg server on your Windows desktop, you can choose between [Xming](https://sourceforge.net/projects/xming/) and [VcXsrv Windows X Server](https://sourceforge.net/projects/vcxsrv/).


## Build

Run the build with:

```sh
make build_unix
```

## Run

Now you can start the emulator:

```sh
./emu.py
```

The emulator has a number of interesting features all documented in the [Emulator](../emulator/index.md) section.

## Building for debugging and hacking in Emulator (Unix port)

Build the debuggable unix binary so you can attach the gdb or lldb.
This removes optimizations and reduces address space randomization.
Beware that this will significantly bloat the final binary
and the firmware runtime memory limit HEAPSIZE may have to be increased.

```sh
DEBUG_BUILD=1 make build_unix
```
