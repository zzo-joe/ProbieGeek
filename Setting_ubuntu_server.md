# Ubuntu server settings
This method is based on Ubuntu Server 20.04LTS

## Installation of Ubuntu Server
Ubuntu Server can be downloaed [here](https://ubuntu.com/download/server).

After downloading "iso" files, create bootable USB drives
You may use "[Rufus](https://rufus.ie/ko/)", a utility that helps format and create bootable USB flash drives



## Managing Users

Using following code and follow directions
```
sudo adduser {user_name}
```

If you want to give a user "sudo" authentication
```
usermod -aG sudo {user_name}
```

If you want to delete a user
```
sudo userdel {user_name}
```

If you want to change user password
```
sudo passwd {user_name}
```
