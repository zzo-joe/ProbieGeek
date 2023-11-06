# User management

### Adding/Deleting users
> Requires ***sudo previlage*** when modifying users
```
# When adding
sudo adduser {USER NAME}

# When deleting
sudo userdel {USER NAME}
```

### Changing pasasword of user
```
sudo passwd {USER NAME}
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
