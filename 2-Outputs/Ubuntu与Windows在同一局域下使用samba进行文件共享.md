### Ubuntu与Windows在同一局域下使用samba进行文件共享

#### a. ubuntu端

1. 安装samba服务

```
sudo apt install samba
```

2. 添加配置

```
sudo gedit /etc/samba/smb.conf

# 在打开的文件末尾插入以下内容
[ubuntu2204]      #这里写什么，windows 链接共享文件夹后， 文件夹名称就显示什么
path = /home/zhengmo/ShareDir  #设置允许访问的目录
available = yes
browseable = yes
public = yes
writable = yes      #共享目录具有写权限
valid users = zhengmo  #设置允许访问samba 共享文件夹的账户名，也即后续windows网络凭据的用户名
```

3. 设置samba账户密码

```
sudo smbpasswd -a <valid users>    
```

4. 设置samba开机启动并重启服务

```
systemctl enable smbd
systemctl restart smbd
```

5. 共享文件夹

右键第二步中允许访问的文件夹

![image-20240605133008551](/home/zhengmo/.config/Typora/typora-user-images/image-20240605133008551.png)

注意勾选Allow others to... 不然windiws端不能添加或删除文件



#### b. windows端

1. 右键此电脑 -> 映射网络驱动器

![屏幕截图 2024-06-05 133119](/home/zhengmo/ShareDir/屏幕截图 2024-06-05 133119.png)

文件夹填写ubuntu端IP地址\共享文件夹名

2. 输入网络凭据，即上面配置的用户名和密码即可