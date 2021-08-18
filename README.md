# 刷X3P

首先保证猫盘（现在不插硬盘）和电脑在同一个局域网内  

Mac前六位请填78C2C0，后面的写猫盘背面的后几位  

SN写猫盘背面的  

刷机完成后，需要拔掉电源，找到猫盘reset（复位）键，按住reset同时插电，保持按住reset 15秒以上再放手，此时猫盘进入刷机状态，静静等待15-20分钟，直到路由器中看到一个名为onespace的设备获取到IP，表明刷机已经完成，在浏览器输入猫盘IP即可进入X3P管理页面，默认账号：admin，密码：123456  

X3P ssh账户：root    密码：Etech12  

# 一键刷群辉脚本

```bash
wget -N --no-check-certificate https://cdn.jsdelivr.net/gh/roadwide/catdrive-syno/install.sh && chmod +x install.sh && bash install.sh
```

# 群晖开启硬盘休眠

```bash
sudo vi /etc/init/syslog-ng.conf
```

定位到 50 行左右（52行）。fi之后，/usr/syno/sbin/synologconfgen || true之前。插入下面代码  

```bash
#scemd bind 
touch /tmp/scemd.log.new || true 
chmod 660 /tmp/scemd.log.new || true 
chown system:log /tmp/scemd.log.new || true 
mount -o bind /tmp/scemd.log.new /var/log/scemd.log || true 
# 
```

重启后去套件中心里安装日志中心工具，过一段时间去查看日志，如果看到有Internal disks woke up from hibernation 日志，就说明硬盘休眠功能正常。