# linux-references


### Building, Compiling and Installing kernel modules/drivers

```
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
