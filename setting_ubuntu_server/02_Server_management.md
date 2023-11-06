# Ethernet set-up 

### Identify ethernet interfaces  
[Tip](https://ubuntu.com/server/docs/network-configuration)

  * Using command "ip"
  ```
  ip a

  1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
      link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
      inet 127.0.0.1/8 scope host lo
         valid_lft forever preferred_lft forever
      inet6 ::1/128 scope host
         valid_lft forever preferred_lft forever
  2: enp0s25: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
      link/ether 00:16:3e:e2:52:42 brd ff:ff:ff:ff:ff:ff link-netnsid 0
      inet 10.102.66.200/24 brd 10.102.66.255 scope global dynamic eth0
         valid_lft 3257sec preferred_lft 3257sec
      inet6 fe80::216:3eff:fee2:5242/64 scope link
         valid_lft forever preferred_lft forever
  ```
  
  * Via Netplan configutaion.
    They reside in "/etc/netplan/" under name of "00-installer-config.yaml"  
  ```
  network:
    version: 2
    renderer: networkd
    ethernets:
      eth_lan0:
        dhcp4: true
        match:
          macaddress: 00:11:22:33:44:55
        set-name: eth_lan0
  ```


### IP addressing  
> Requires ***sudo previlage*** when editting or applying network configuration changes
* DHCP setting  
```
network:
  version: 2
  renderer: networkd
  ethernets:
    enp3s0:
      dhcp4: true
```  
* Static IP address setting
> Note: Be delicate with spaces
```
network:
  ethernets:
    eth0:
      dhcp4: no
      addresses: [10.10.10.2/24]
      gateway4: 10.10.10.129
      nameservers:
          search: [mydomain, otherdomain]
          addresses: [10.10.10.1, 1.1.1.1]

```  
__YOU SHOULD APPLY ABOVE CHANGES BY FOLLOWING CODE__  
```
sudo netplan apply
```  

# SSH service configuration 
[tip](https://smoh.tistory.com/m/337)  
> Requires ***sudo previlage*** when editting or applying changes in ssh service
* The Secure Shell (SSH) protocol is a method for securely sending commands to a computer over an unsecured network. SSH uses cryptography to authenticate and encrypt connections between devices.
Explaination credit: [Cloudflare](https://www.cloudflare.com/ko-kr/learning/access-management/what-is-ssh/)  

* SSH service settings can be altered by following code
  > You may use your preferable script editor
  ```
  sudo nano /etc/ssh/sshd_config
  ```
* Change Port information
  ```
  
  ```

__YOU SHOULD APPLY ABOVE CHANGES BY FOLLOWING CODE__  
```
sudo service sshd restart
```  

# Connecting Synology NAS to your server 
[tip](https://saywebsolutions.com/blog/mounting_synology_nas_shared_folder_nfs_ubuntu_16_10)  

### Settings should be done in Synology NAS for further connection.  
* See [How to access files on Synology NAS within the local network (NFS)](https://kb.synology.com/en-ca/DSM/tutorial/How_to_access_files_on_Synology_NAS_within_the_local_network_NFS)
    > *Go to Control Panel > File Services > NFS (for DSM 7.0 and above)  
    > *Enable NFS services  
    > *Go to Control Panel > Shared Folder  
    > *Select the shared folder that you want to access with your NFS client and click Edit.
    > *Go to NFS Permissions and click Create.
    > *Add client (IP address of your server) and save


### Packages should be installed in your server
```
sudo apt install nfs-common
```
### Connect NAS to server

```
# You should be aware of IP address of both your server and NAS
sudo mount {NAS_IP_address}:{Volume_you_want_to_connect} {Location_you_want_to_connect} nfs

# Add NFS settings using your favorite text editor
sudo nano /etc/fstab

{NAS_IP_address}:{Volume_you_want_to_connect} {Location_you_want_to_connect} nfs rsize=8192,wsize=8192,timeo=14,intr
```
