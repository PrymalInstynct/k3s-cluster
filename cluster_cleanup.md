sudo -i

sed -i '/deb cdrom/d' /etc/apt/sources.list && apt update && apt install -y kitty-terminfo vim curl gdisk parted && echo "zimmermanc ALL=(ALL) NOPASSWD:ALL" | tee /etc/sudoers.d/zimmermanc

swapoff -a
vim /etc/fstab
    - Delete Bottom 2 lines
fdisk /dev/sda
    - d
    - 3
    - w

apt -y install systemd-resolved
vim /etc/systemd/resolved.conf
    - DNS=10.10.1.31 10.10.1.32


rm -rf /var/lib/rook
DISK="/dev/nvme0n1"
sgdisk --zap-all $DISK
dd if=/dev/zero of="$DISK" bs=1M count=100 oflag=direct,dsync
blkdiscard $DISK
partprobe $DISK

reboot