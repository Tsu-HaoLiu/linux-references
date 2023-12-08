# linux-references


### Building, Compiling and Installing kernel modules/drivers
https://askubuntu.com/questions/1388115/how-do-i-update-my-kernel-to-the-latest-one
```Shell
# You will need to install headers
sudo apt install linux-headers-$(uname -r)

# Kernal you are looking to install from https://www.kernel.org/
wget https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-6.5.9.tar.xz
# Extract kernel source code
tar xvf linux-6.5.9.tar.xz

# Required Packages for building kernel
sudo apt-get install git fakeroot build-essential ncurses-dev xz-utils libssl-dev bc flex libelf-dev bison

# cd into module you want to build
cd linux-6.5.9/drivers/net/wireless/intel/ipw2xxx

# Make the module
# Possible error if you don't have headers installed
# make: /lib/modules/$(uname -r)/buildL No such file or diectory. Stop
make -C /lib/modules/$(uname -r)/build M=$(pwd) modules

# After building find your old module/driver (if its runnning) 
lsmod | grep ipw 
lspci -v

# and stop it (or start it)
sudo modprobe -r ipw2xxx
sudo modprobe ipw2xxx

# insert module
sudo insmod ipw2200.ko

# Possible error if there are missing symbols in your build
# insmod: ERROR: could not insert module some-module.ko: Unknown symbol in module
# Check logs
dmesg | tail
```

### Build Linux Kernel From Scratch
https://phoenixnap.com/kb/build-linux-kernel

https://www.kernel.org
```Shell
# Download source code from offical kernel site
wget https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-6.6.tar.xz

# Extract the Source Code
tar xvf linux-6.6.tar.xz

# Required Packages for building kernel
sudo apt-get install git fakeroot build-essential ncurses-dev xz-utils libssl-dev bc flex libelf-dev bison

# Enter directory
cd linux-6.6

# Copy config file
cp -v /boot/config-$(uname -r) .config

# Make changes to config file
make menuconfig

# Build kernel
make
# Errors .tmp_vmlinux.btf: pahole (pahole is not available)
# Failed to generate BTF for vmlinux
# https://stackoverflow.com/questions/61657707/btf-tmp-vmlinux-btf-pahole-pahole-is-not-available
@ need to restart PC after installing

# Install required modules
sudo make INSTALL_MOD_STRIP=1 modules_install

# Install kernel
sudo make install

```

### Uninstalling Built Linux Kernel From Source
https://askubuntu.com/questions/594443/how-can-i-remove-compiled-kernel
```Shell
# Locate boot folder
ll /boot/

# Remove files
sudo rm <file>
# /boot/vmlinuz*KERNEL-VERSION*
# /boot/initrd*KERNEL-VERSION*
# /boot/System-map*KERNEL-VERSION*
# /boot/config-*KERNEL-VERSION*
# /lib/modules/*KERNEL-VERSION*/
# /var/lib/initramfs/*KERNEL-VERSION*/

# Update grub config
sudo update-grub2
```


### Searching for new headers
```Shell
apt search linux-headers | grep headers
```


