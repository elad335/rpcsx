## Building


### The dependencies for Debian-like distributions.

```   
sudo apt install build-essential cmake libunwind-dev libglfw3-dev libvulkan-dev vulkan-validationlayers-dev spirv-tools glslang-tools libspirv-cross-c-shared-dev
```

### The dependencies for Fedora distributions:

```
sudo dnf install cmake libunwind-devel glfw-devel vulkan-devel vulkan-validation-layers-devel spirv-tools glslang-devel gcc-c++ gcc spirv-tools-devel xbyak-devel
```

### The dependencies for Arch distributions:

```
sudo pacman -S libunwind glfw-x11 vulkan-devel glslang
```
> Side note you will need to pull ``spirv-cross`` from the AUR for now so do the following
```
sudo pacman -S --needed git base-devel && git clone https://aur.archlinux.org/yay.git && cd yay && makepkg -si
```
```
yay -S spirv-cross
```

## Getting spriv-cross on Fedora and Arch Linux

```
git clone https://github.com/KhronosGroup/SPIRV-Cross && cd SPIRV-Cross && mkdir build && cd build && cmake .. && cmake --build . && sudo make install
```
> **Warning** <br/>
> Fedora will compile to a point and then error out
> Arch will have to use xbyak from the aur for now

## Cloning the Repo

```
git clone --recursive https://github.com/RPCSX/rpcsx && cd rpcsx
```
```
git submodule update --init --recursive
```  
## How to compile the emulator
   
```
mkdir -p build && cd build && cmake .. && cmake --build .
```

## How to create a Virtual HDD

> The PS4 has a case-insensitive filesystem. To create the Virtual HDD, do the following:
 
```
truncate -s 512M ps4-hdd.exfat

mkfs.exfat -n PS4-HDD ./ps4-hdd.exfat

mkdir ps4-fs

sudo mount -t exfat -o uid=`id -u`,gid=`id -g` ./ps4-hdd.exfat ./ps4-fs
```

## How to run samples and games
   
See the Commands of `rpcsx-os` (`-h` argument), or join the [Discord](https://discord.gg/t6dzA4wUdG) for help.

You can run the emulator with some samples using this command:
   
```
rm -f /dev/shm/rpcsx-* && ./rpcsx-os --mount  "<path to fw>/system" "/system" --mount "<path to 'game' root>" /app0 /app0/some-test-sample.elf [<args for test elf>...]
```

## Creating a log

You can use this flag if you encountered a segfault for debugging purposes.
    
```
--trace
``` 
    
You can redirect all log messages to a file by appending this command:

```
&>log.txt
```
