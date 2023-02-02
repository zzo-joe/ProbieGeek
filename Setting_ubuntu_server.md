# Ubuntu server settings
This method is based on Ubuntu Server 20.04LTS

## Installation of Ubuntu Server
Ubuntu Server can be downloaed [here](https://ubuntu.com/download/server).

After downloading "iso" files, create bootable USB drives
You may use "[Rufus](https://rufus.ie/ko/)", a utility that helps format and create bootable USB flash drives



## Managing Users

#### Using following code and follow directions
```
sudo adduser {user_name}
```
* Assign and confirm a password for the new user
* Enter any additional information about the user


#### If you want to give a user "sudo" authentication
```
usermod -aG sudo {user_name}
```

#### If you want to delete a user
```
sudo userdel {user_name}
```

#### If you want to change user password
```
sudo passwd {user_name}
```

## Procedure

1. Install ubuntu server
> Reformat boot disk into ext4 format
> 
> Set disk as you want (RAID settings, folder settings, etc.)

2. Change basic servers [Tip](https://memostack.tistory.com/217)

> Not manditory
> 
> Changing server might boost your ubuntu update or upgrade speed
> 
> Requires sudo authentication
> 
```
sudo sed -i 's/kr.archive.ubuntu.com/mirror.kakao.com/g' /etc/apt/source.list
```

3. Set up ethernet [Tip](https://medium.com/@it_dayeon/ubuntu-18-04-고정-ip-설정하기-54671dec8055)
> Find the name of your ehternet
> 
> Use your favorite text editor to add information in network-config
> 
> Apply netplan using sduo authentication
> 
```
sudo nano /etc/netplan/network-config.yaml
# or
sudo vi /etc/netplan/network-config.yaml

sudo netplan apply
```

4. Run update

```
sudo apt-get -y update
```

5. Change ssh service setting [Tip](https://smoh.tistory.com/m/337)

```
sudo nano /etc/ssh/sshd_config

```
> Change port
> 
> PermitRootLogin >> Yes
> 
> ChallengeResponseAuthentication >> Yes

```
sudo service sshd restart
````

6. Setup and connect synology NAS [Tip](https://saywebsolutions.com/blog/mounting_synology_nas_shared_folder_nfs_ubuntu_16_10)

* Some setting should be done in Synology NAS

Reference: [How to access files on Synology NAS within the local network (NFS)](https://kb.synology.com/en-ca/DSM/tutorial/How_to_access_files_on_Synology_NAS_within_the_local_network_NFS)

> Go to Control Panel > File Services > NFS (for DSM 7.0 and above)
> 
> Enable NFS services
> 
> Go to Control Panel > Shared Folder.
> 
> Select the shared folder that you want to access with your NFS client and click Edit.
> 
> Go to NFS Permissions and click Create.


* Some packages should be installed on server

```
sudo apt install nfs-common
```


* Connect NAS to server

```
# You should be aware of IP address of both your server and NAS
sudo mount {NAS_IP_address}:{Volume_you_want_to_connect} {Location_you_want_to_connect}

# Add NFS settings using your favorite text editor
sudo nano /etc/fstab

{NAS_IP_address}:{Volume_you_want_to_connect} {Location_you_want_to_connect} nfs rsize=8192,wsize=8192,timeo=14,intr
```

