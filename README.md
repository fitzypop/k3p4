# k3p4

K3P4 - 4 node Raspberry Pi 4 Cluster using k3s

List of hostnames for each board

k3p4m = master k3s node
k3p4w1 = worker k3s node #1
k3p4w2 ...
k3p4w3 ...

## Setting up Raspberry Pis

All pis in my build are 'Raspberry Pi Model B 8gb arm64' boards, with 32gb sandisk cards.

I'm still figuring out k3s and networking and everything else.

`sudo apt install curl vim python3-pip`

### Patch Configs for k3s

```sh
# Add cgroups
sudo vim /boot/firmware/cmdline.txt

# Add this to the existing oneliner
cgroup_memory=1 cgroup_enable=memory
```

### Turn off / remove bluetooth

`sudo vim /boot/firmware/config.txt`

add this line `dtoverlay=disable-bt`

then run these lines

```sh
sudo systemctl disable hciuart.service
sudo systemctl disable bluetooth.service
sudo apt purge bluez
sudo apt autoremove
sudo reboot
```

## Install k3s on master node

`curl -sfl https://get.k3s.io | K3S_KUBECONFIG_MODE="644" sh -s`
