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
cd linux-6.5.9/drivers/net/wireless/intel/ipw2x00

# Make the module
make -C /lib/modules/$(uname -r)/build M=$(pwd) modules

```
