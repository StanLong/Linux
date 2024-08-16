# 部署内网yum存储库

## 一、服务端操作

1. 准备工作

   ```shell
   # 关闭防火墙和 selinux
   [root@node04 ~]# systemctl disable --now firewalld
   [root@node04 ~]# setenforce 0
   setenforce: SELinux is disabled
   
   # 安装 yum-utils
   [root@node04 ~]# yum install -y yum-utils createrepo
   
   # 查看仓库并缓存仓库信息
   [root@node04 ~]# yum repolist
   repo id                              repo name                                                   status
   base/7/x86_64                        CentOS-7 - Base - mirrors.aliyun.com                        10,072
   extras/7/x86_64                      CentOS-7 - Extras - mirrors.aliyun.com                         526
   updates/7/x86_64                     CentOS-7 - Updates - mirrors.aliyun.com                      6,173
   repolist: 16,771
   [root@node04 ~]# yum makecache
   base                                                                            | 3.6 kB  00:00:00     
   extras                                                                          | 2.9 kB  00:00:00     
   updates                                                                         | 2.9 kB  00:00:00     
   (1/4): extras/7/x86_64/other_db                                                 | 154 kB  00:00:00     
   (2/4): extras/7/x86_64/filelists_db                                             | 305 kB  00:00:00     
   (3/4): updates/7/x86_64/other_db                                                | 1.6 MB  00:00:03     
   (4/4): updates/7/x86_64/filelists_db                                            |  15 MB  00:00:23     
   Metadata Cache Created
   
   # 查找包组信息
   [root@node04 ~]# find /var -name "*comps*"
   /var/cache/yum/x86_64/7/base/a4e2b46586aa556c3b6f814dad5b16db5a669984d66b68e873586cd7c7253301-c7-x86_64-comps.xml.gz
   
   # 安装nginx并创建三个工作目录
   # 默认情况Centos7中无Nginx的源rpm，需要添加Nginx的源RPM
   [root@node04 ~]# yum -y install epel-release # 添加Nginx源
   [root@node04 ~]# yum -y update               # 更新源
   [root@node04 ~]# yum -y install nginx        # 安装Nginx 
   [root@node04 ~]# mkdir -p /usr/share/nginx/html/repo/{base,updates,extras} # 软件最终存储在这三个目录里, 注意这三个目录是根据  yum repolist 命令中看到的 repo name 来确定的
   ```

2. 同步软件包

   ```shell
   # 同步软件包， 这里把同步命令封装成脚本
   #!/bin/bash
   
   # 定义需要同步的软件仓库，多个仓库已空格分隔
   repolist="base updates extras"
   for i in ${repolist}
   do
       # 从互联网仓库同步软件，并保存输出日志到 /var/log/reposync.log
       reposync -g -n -m --delete --repoid=$i --download-metadata -p /usr/share/nginx/html/repo &> /var/log/reposync.log
       # 创建仓库元数据信息
       createrepo /usr/share/nginx/html/repo/$i
   done
   # 为存在包组的存储库创建软件包组信息，不存在则不需要
   createrepo -g comps.xml /usr/share/nginx/html/repo/base
   --------------------------------------------------------------------------------------------------------------------
   # reposync 参数说明
   -g 表示删除下载后没有通过GPG检查的软件包
   -n 仅同步仓库中最新的软件
   -m 表示下载包组信息
   --delete 用于删除本地存储库中存在的但在线存储库中没有的软件包
   --repoid 指定了要同步的仓库
   --download-metadata 下载包的元数据信息
   -p 指定下载目录
   
   ```

3. 结果验证

   ```shell
   [root@node04 ~]# cd /usr/share/nginx/html/repo/
   [root@node04 repo]# ll
   total 0
   drwxr-xr-x 4 root root 150 2024-08-01 23:57:25 base
   drwxr-xr-x 4 root root  38 2024-08-01 23:55:10 extras
   drwxr-xr-x 4 root root  38 2024-08-01 23:54:42 updates
   [root@node04 repo]# du -sh *
   9.0G	base
   324M	extras
   3.4G	updates
   [root@node04 repo]# tree -d -L 2 .
   .
   ├── base
   │   ├── Packages
   │   └── repodata
   ├── extras
   │   ├── Packages
   │   └── repodata
   └── updates
       ├── Packages
       └── repodata
   
   # 表示仓库已经创建完成
   ----------------------------------------------------------------------------
   # 编辑nginx配置
   vim /etc/nginx/nginx.conf
   # 在 location块中加入这行配置
   location / {
              autoindex on;
           }
   
   # 启动nginx
   [root@node04 repo]# systemctl enable --now nginx
   
   # 在网页中访问如下地址验证
   http://node04/repo/base/
   http://node04/repo/extras/
   http://node04/repo/updates/
   ```

## 二、客户端操作

1. 配置yum源

   ```shell
   [root@node03 ~]# vim /etc/yum.repos.d/local.repo
   
   [BaseOS]
   baseurl=http://node04/repo/base/
   enabled=1
   gpgcheck=0
   
   [Extras]
   baseurl=http://node04/repo/extras/
   enabled=1
   gpgcheck=0
   
   [Updates]
   baseurl=http://node04/repo/updates/
   enabled=1
   gpgcheck=0
   ```

2. 结果验证

   ```shell
   [root@node03 yum.repos.d]# yum repolist -v
   Loading "fastestmirror" plugin
   Config time: 0.195
   Yum version: 3.4.3
   Repository 'BaseOS' is missing name in configuration, using id
   Repository 'Extras' is missing name in configuration, using id
   Repository 'Updates' is missing name in configuration, using id
   BaseOS                                                                          | 3.6 kB  00:00:00     
   Extras                                                                          | 2.9 kB  00:00:00     
   Updates                                                                         | 2.9 kB  00:00:00     
   (1/4): BaseOS/group_gz                                                          | 153 kB  00:00:00     
   (2/4): Extras/primary_db                                                        | 136 kB  00:00:00     
   (3/4): Updates/primary_db                                                       | 2.1 MB  00:00:00     
   (4/4): BaseOS/primary_db                                                        | 6.1 MB  00:00:00     
   Determining fastest mirrors
   Setting up Package Sacks
   pkgsack time: 0.006
   Repo-id      : BaseOS
   Repo-name    : BaseOS
   Repo-revision: 1722556511
   Repo-updated : Thu Aug  1 23:57:25 2024
   Repo-pkgs    : 10,072
   Repo-size    : 8.9 G
   Repo-baseurl : http://node04/repo/base/
   Repo-expire  : 21,600 second(s) (last: Fri Aug  2 00:19:36 2024)
     Filter     : read-only:present
   Repo-filename: /etc/yum.repos.d/local.repo
   
   Repo-id      : Extras
   Repo-name    : Extras
   Repo-revision: 1722556508
   Repo-updated : Thu Aug  1 23:55:10 2024
   Repo-pkgs    : 278
   Repo-size    : 322 M
   Repo-baseurl : http://node04/repo/extras/
   Repo-expire  : 21,600 second(s) (last: Fri Aug  2 00:19:36 2024)
     Filter     : read-only:present
   Repo-filename: /etc/yum.repos.d/local.repo
   
   Repo-id      : Updates
   Repo-name    : Updates
   Repo-revision: 1722556454
   Repo-updated : Thu Aug  1 23:54:42 2024
   Repo-pkgs    : 1,766
   Repo-size    : 3.4 G
   Repo-baseurl : http://node04/repo/updates/
   Repo-expire  : 21,600 second(s) (last: Fri Aug  2 00:19:36 2024)
     Filter     : read-only:present
   Repo-filename: /etc/yum.repos.d/local.repo
   
   repolist: 12,116
   [root@node03 yum.repos.d]# 
   ```

   

