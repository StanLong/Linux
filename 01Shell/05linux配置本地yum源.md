# Linux配置本地yum源

```shell
mkdir -p /dvd/

mount -o loop,ro rhel-server-7.9-x86_64-dvd.iso /dvd/

cd /etc/yum.repos.d/
vim RHEL7.9.repo


[rhels7.9-x86_64]
name=yum repository for /dvd
baseurl=file:///dvd
enabled=1
gpgcheck=0
 
[rhels7.9-x86_64-addons-ResilientStorage]
name=yum repository for /dvd/addons/ResilientStorage
baseurl=file:///dvd/addons/ResilientStorage
enabled=1
gpgcheck=0
 
[rhels7.9-x86_64-addons-HighAvailability]
name=yum repository for /dvd/addons/HighAvailability
baseurl=file:///dvd/addons/HighAvailability
enabled=1
```

