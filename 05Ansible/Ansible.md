# Ansible

https://www.yuque.com/gugujun/qr3rlq/zv97zcso8yveak9n

https://getansible.com/

## 一、Ansible

Ansible是一款基于`Python` 开发的开源自动化工具，主要用于配置管理、应用部署、任务自动化和持续交付。它由 `Red Hat` 公司维护， 采用无代理架构（无需在目标主机上安装客户端），通过 `SSH` 进行通信，简化了大规模系统的管理。

2、特点

任务执行模式

- ad-hoc模式(点对点模式)
  　　使用单个模块，支持批量执行单条命令。ad-hoc 命令是一种可以快速输入的命令，而且不需要保存起来的命令。**就相当于bash中的一句话shell。**
- playbook模式(剧本模式)
  　　是Ansible主要管理方式，也是Ansible功能强大的关键所在。**playbook通过多个task集合完成一类功能**，如Web服务的安装部署、数据库服务器的批量备份等。可以简单地把playbook理解为通过组合多条ad-hoc操作的配置文件。

安装

```shell
yum install epel-release -y
yum install ansible -y

安装目录如下(yum安装)：
　　配置文件目录：/etc/ansible/
　　执行文件目录：/usr/bin/
　　Lib库依赖目录：/usr/lib/pythonX.X/site-packages/ansible/
　　Help文档目录：/usr/share/doc/ansible-X.X.X/
　　Man文档目录：/usr/share/man/man1/
```

ansible 命令格式

```
ansible <host-pattern> [-f forks] [-m module_name] [-a args]
```

也可以通过`ansible -h`来查看帮助，下面我们列出一些比较常用的选项，并解释其含义：

```
-a MODULE_ARGS　　　#模块的参数，如果执行默认COMMAND的模块，即是命令参数，如： “date”，“pwd”等等
-k，--ask-pass #ask for SSH password。登录密码，提示输入SSH密码而不是假设基于密钥的验证
--ask-su-pass #ask for su password。su切换密码
-K，--ask-sudo-pass #ask for sudo password。提示密码使用sudo，sudo表示提权操作
--ask-vault-pass #ask for vault password。假设我们设定了加密的密码，则用该选项进行访问
-B SECONDS #后台运行超时时间
-C #模拟运行环境并进行预运行，可以进行查错测试
-c CONNECTION #连接类型使用
-f FORKS #并行任务数，默认为5
-i INVENTORY #指定主机清单的路径，默认为/etc/ansible/hosts
--list-hosts #查看有哪些主机组
-m MODULE_NAME #执行模块的名字，默认使用 command 模块，所以如果是只执行单一命令可以不用 -m参数
-o #压缩输出，尝试将所有结果在一行输出，一般针对收集工具使用
-S #用 su 命令
-R SU_USER #指定 su 的用户，默认为 root 用户
-s #用 sudo 命令
-U SUDO_USER #指定 sudo 到哪个用户，默认为 root 用户
-T TIMEOUT #指定 ssh 默认超时时间，默认为10s，也可在配置文件中修改
-u REMOTE_USER #远程用户，默认为 root 用户
-v #查看详细信息，同时支持-vvv，-vvvv可查看更详细信息
```



| 选项             | 全称       | 作用                                                         | 示例 |
| ---------------- | ---------- | ------------------------------------------------------------ | ---- |
| -v  / -vv / -vvv | --verbose  | 输出详细日志 (-vvv 最详细)                                   | -vv  |
| -k               | --ask-pass | ask for SSH password。登录密码，提示输入SSH密码而不是假设基于密钥的验证 | -k   |
|                  |            |                                                              |      |
|                  |            |                                                              |      |

ansible 常用命令





### 一、Ansible 介绍

`Ansible`是一款基于`Python`开发的开源自动化工具，主要用于配置管理、应用部署、任务自动化和持续交付。它由`Red Hat`公司维护，采用无代理架构（无需在目标主机上安装客户端），通过`SSH`进行通信，简化了大规模系统的管理。

日常生活中拧螺丝，我们可以选择使用螺丝刀一点点的拧好。我们也可以选择用电钻（电动螺丝刀）轻松搞定。两者都能达到我们的目的，选择哪个工具一目了然。

`Ansible`就好比这里的电动螺丝刀。使用传统的`shell`命令一台台去操控服务器，固然可以完成目的。但是在目标服务器过多、配置过于繁杂的情况下使用`Ansible`一定是更好的选择。

**官方文档：**`**https://docs.ansible.org.cn/ansible/latest/index.html**`

#### Ansible 的特点

1. **无代理架构（部署简单）**

1. 1. 直接通过`SSH`或`WinRM`管理目标主机，无需安装额外的客户端

1. **基于模块化设计**

1. 1. `Ansible`本身仅提供框架，真正的批量操作由模块实现。支持的模块成千上万，可解决大部分场景

1. **声明式**`**YAML**`**语法**

1. 1. 使用`Playbook`定义自动化任务，直观易读，方便完成复杂任务

1. **跨平台支持**

1. 1. 各平台设备都可被`Ansible`管理

1. **可扩展**

1. 1. 支持`API`及自定义模块，可通过`Python`进行扩展

1. **幂等性**

1. 1. 重复执行任务不会导致系统状态异常，确保操作一致性

#### Ansible 模块化

`Ansible`本身像是一个工具箱，工具箱里存放着许许多多的工具，这些工具就是`Asnsible`的模块。根据不同场景，我们要选择最合适自己的工具（模块）。

![img](https://cdn.nlark.com/yuque/0/2025/png/42713143/1743149589462-fa78f5b1-03e7-441d-a9d4-d4af8f95dffe.png)

#### `Ansible`学习路线

[📎Ansible 学习路线.xmind](https://www.yuque.com/attachments/yuque/0/2025/xmind/42713143/1743150032830-724785f3-6aa4-4052-8d55-8ada0fab30f0.xmind)

![img](https://cdn.nlark.com/yuque/0/2025/png/42713143/1743150072211-5d21f69d-3500-4cde-9b0d-88372e3c8b8c.png)

#### Ansible 执行过程

![img](https://cdn.nlark.com/yuque/0/2025/png/42713143/1743151442924-f3829e62-f962-480d-b634-045d5a01d427.png)

1. 用户发出`Ansible`命令（`Ad-Hoc`或`Playbook`）
2. `Ansible`主程序加载自己的配置文件`/etc/ansible/ansible.cfg`
3. 读取主机清单中的设备`IP`或域名及变量
4. 调用`Ansible`命令中指定的模块，通过`Ansible`将模块参数生成对应的临时`python`脚本，传输至目标服务器
5. 对应目标主机的执行用户的家目录中出现`.ansible/tmp/xxx/xxx.py`文件，给改文件赋予可执行权限。执行该脚本并返回结果

### 二、 Ansible 入门

#### 安装`Ansible`

```bash
yum install -y ansible
&&
[root@openEuler ~]# ansible --version
ansible 2.9.27
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3.9/site-packages/ansible
  executable location = /usr/bin/ansible
  python version = 3.9.9 (main, Dec 28 2023, 13:48:32) [GCC 10.3.1]
```

`Ansible`分为两个包：

1. `ansible 2.9`：完整的`ansible`安装包，包含大部分常见的模块
2. `ansible-core`：`ansible`的核心安装包，缺少很多功能模块，需要单独安装。

#### `Ad-Hoc`

`Ad-Hoc`命令是`Ansible`提供的一种快速执行简单任务的命令行工具，它允许用户在不编写完整`playbook`的情况下直接执行单条命令，多用于测试及学习。

**基本语法**

```bash
ansible <host-pattern> -m <module-name> -a "<module-arguments>" [options]
```

- `host-pattern`：指定目标主机或主机组（如：`all`、`webservers`、`192.168.1.*`）
- 模块（`-m`）：指定要使用的`Ansible`模块
- 模块参数（`-a`）：传递给模块的参数

**常用选项列表**

| **选项**                                  | **全称**                | **作用**                                                     | **示例**                           |
| ----------------------------------------- | ----------------------- | ------------------------------------------------------------ | ---------------------------------- |
| `**-i <路径>**`                           | `**--inventory**`       | **指定自定义 Inventory 文件**                                | `**-i /etc/ansible/my_hosts.ini**` |
| `**-m <模块名>**`                         | `**--module-name**`     | **指定要使用的模块（如** `**command**`**,** `**shell**`**,** `**copy**` **等）** | `**-m shell**`                     |
| `**-a "<参数>"**`                         | `**--args**`            | **传递给模块的参数**                                         | `**-a "ls -l /tmp"**`              |
| `**-u <用户名>**`                         | `**--user**`            | **指定 SSH 连接用户**                                        | `**-u root**`                      |
| `**-k**`                                  | `**--ask-pass**`        | **提示输入 SSH 密码（默认密钥认证失败时使用）**              | `**-k**`                           |
| `**-b**`                                  | `**--become**`          | **使用特权升级（如** `**sudo**`**）**                        | `**-b**`                           |
| `**-K**`                                  | `**--ask-become-pass**` | **提示输入特权密码（如 sudo 密码）**                         | `**-K**`                           |
| `**--become-user=<用户>**`                | **-**                   | **指定特权升级的目标用户（需配合** `**-b**`**）**            | `**--become-user=postgres**`       |
| `**-f <数量>**`                           | `**--forks**`           | **设置并行执行的主机数（默认 5）**                           | `**-f 10**`                        |
| `**-l <主机模式>**`                       | `**--limit**`           | **限制执行的主机范围（支持通配符）**                         | `**-l "web\*"**`                   |
| `**-v**` **/** `**-vv**` **/** `**-vvv**` | `**--verbose**`         | **输出详细日志（**`**-vvv**` **最详细）**                    | `**-vv**`                          |
| `**--list-hosts**`                        | **-**                   | **仅列出匹配的主机，不执行命令**                             | `**--list-hosts**`                 |
| `**--check**`                             | **-**                   | **模拟执行（Dry Run），不实际修改系统**                      | `**--check**`                      |
| `**--diff**`                              | **-**                   | **显示文件变更的差异（常用于** `**copy**`**/**`**template**` **模块）** | `**--diff**`                       |
| `**-e "<变量>"**`                         | `**--extra-vars**`      | **设置额外变量（支持 JSON/YAML 格式）**                      | `**-e "user=admin"**`              |
| `**-o**`                                  | `**--one-line**`        | **简化输出为单行格式**                                       | `**-o**`                           |
| `**-B <秒数>**`                           | `**--background**`      | **后台异步执行任务（需配合** `**-P**` **轮询）**             | `**-B 3600 -P 60**`                |
| `**-t <目录>**`                           | `**--tree**`            | **将输出结果保存到指定目录（按主机名分文件）**               | `**-t /tmp/ansible-logs**`         |

**类比**

```bash
ansible all -m yum -a "name=vim-enhanced state=present"
name:包的名称
state=present:表示安装（如果已安装则不做操作）
&&
yum install -y vim
```

- `ansible`命令中的`-m yum`等同于`shell`命令中的`yum`命令
- `ansible`命令中的`-a state=present`等同于`shell`命令中的`install`
- `ansible`命令中的`-a name=vim-enhanced`等同于`shell`命令中的`vim`

#### Ansible 主配置文件

```bash
[defaults]	#通用配置项
# 默认Inventory文件路径（主机清单文件）
# inventory = /etc/ansible/hosts

# 远程连接用户（默认当前用户）
# remote_user = root

# 是否提示SSH密码（默认False，建议使用密钥认证）
# ask_pass = False

# 是否检查远程主机SSH密钥（生产环境建议True）
# host_key_checking = False

# 日志文件路径（需确保写入权限）
# log_path = /var/log/ansible.log

# 并行执行任务的工作进程数（默认5）
# forks = 5

# 模块执行超时时间（秒）
# timeout = 10

# 默认模块名称（command/shell等）
# module_name = command

# 是否收集主机facts信息（默认True）
# gathering = smart

# 临时文件存放目录
# remote_tmp = ~/.ansible/tmp


[privilege_escalation]	#提权配置项
# 是否启用权限提升（sudo/su等）
# become = True

# 权限提升方式（sudo/su/pbrun等）
# become_method = sudo

# 提升到的目标用户（默认root）
# become_user = root

# 是否提示become密码（默认False）
# become_ask_pass = False


[ssh_connection]	#ssh连接的配置项
# 启用SSH管道加速（需目标机sudoers禁用requiretty）
# pipelining = True

# 优先使用SCP而非SFTP传输文件
# scp_if_ssh = True

# SSH连接重试次数
# retries = 3


[persistent_connection]	#持久连接配置项
###
ansible连接时需要创建TCP套接字执行SSH任务，当任务结束后就会立即关闭TCP套接字。但是在使用剧本的情况下，就会导致一会关闭一会开启的现象发生，导致资源浪费。所以持久连接，就是创建一个套接字，后续的任务就在一定时间内一直走
###
# 持久化SSH连接超时时间（秒）
# timeout = 30

# 连接保持间隔（秒）
# idle_timeout = 15


[galaxy]
# Ansible Galaxy服务器地址
# server = https://galaxy.ansible.com

# 安装Role时的API密钥
# api_key = xxxxx


[colors]
# 输出颜色配置（成功/失败/警告等）
# highlight = white
# warn = bright purple
# error = red
# ok = green
# changed = yellow
```

**为什么主配置文件里的内容都被注释了？**

- `ansible`的所有配置参数都有内置的默认值。
- 用户只需注释并修改需要自定义的配置即可。
- 该设计避免了配置文件的冗余，用户只关注需要覆盖的配置。

#### Ansible 主机清单(静态)

主机清单（Inventory）是 Ansible 的核心配置文件，用于定义**管理哪些主机**以及如何分组。**一个主机可以隶属于多个不同的组。**

默认主机清单文件路径：`/etc/ansible/hosts`（由`/etc/ansible/ansible.cfg` 定义）或通过`-i`指定自定义文件。

**主机清单基本规则**

```bash
###	主机组以[header]开头，这是主机组的名称
###	可以使用主机名/域名或IP地址标识目标主机
###	没有分组的主机需要在所有的主机组之前定义
```

**默认组**

即使主机清单中没有定义任何组，`ansible`也会创建两个默认组：

- `all`：该默认组包含所有主机。
- `ungrouped`：该组包含单独的主机。

**例如：**

- `mail.example.com`属于`all`和`ungrouped`
- `foo.example.com`属于`all`和`webservers`

```bash
mail.example.com

[webservers]
foo.example.com
bar.example.com

[dbservers]
one.example.com
two.example.com
three.example.com
```

#####  范例（1）：

现有四台主机`192.168.100.10`、`192.168.100.11`、`192.168.100.12`、`192.168.100.13`。其中`192.168.100.10`、`192.168.100.11`属于`web_servers`组，`192.168.100.12`、`192.168.100.13`属于`db_servers`组。

现使用管理节点通过`Ansible`的`ping`模块测试：

1. 配置主机清单：

```bash
[root@openEuler ~]# vim /etc/ansible/hosts
[web_servers]
192.168.100.10
192.168.100.11
[db_servers]
192.168.100.12
192.168.100.13
```

1. 使用命令进行`ping`模块测试：

出现如下回显：

- - 由于`Ansible`在执行任何命令时都会先通过`SSH`连接目标主机，而首次通过`SSH`连接主机时，需要进行指纹确认，但`Ansible`默认无法交互式输入`yes`，导致任务卡住并失败。

```bash
[root@openEuler ~]# ansible all -m ping
The authenticity of host '192.168.100.11 (192.168.100.11)' can't be established.
ED25519 key fingerprint is SHA256:1KedmteyduIBZIaTnrLBniBK/+VZMEUyTsuhhliETPc.
This key is not known by any other names
The authenticity of host '192.168.100.10 (192.168.100.10)' can't be established.
ED25519 key fingerprint is SHA256:1KedmteyduIBZIaTnrLBniBK/+VZMEUyTsuhhliETPc.
This key is not known by any other names
The authenticity of host '192.168.100.12 (192.168.100.12)' can't be established.
ED25519 key fingerprint is SHA256:1KedmteyduIBZIaTnrLBniBK/+VZMEUyTsuhhliETPc.
This key is not known by any other names
The authenticity of host '192.168.100.13 (192.168.100.13)' can't be established.
ED25519 key fingerprint is SHA256:1KedmteyduIBZIaTnrLBniBK/+VZMEUyTsuhhliETPc.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

​	解决方法（1）：

- - 提前在控制节点上手动`SSH`到每个目标主机，并输入`yes`确认指纹：

```bash
ssh root@192.168.100.10  # 首次连接时输入yes
ssh root@192.168.100.11  # 重复操作所有主机
```

​	解决方法（2）：

- - 禁止严格主机密钥检查（测试环境适用）

```bash
# 临时生效（命令行）
ansible all -m ping --ssh-common-args='-o StrictHostKeyChecking=no'

# 永久生效（编辑/etc/ansible/ansible.cfg）
[defaults]
host_key_checking = False

# 变量的方式（编辑/etc/ansible/hosts）
[web_servers]
192.168.100.10 ansible_ssh_common_args='-o StrictHostKeyChecking=no'
192.168.100.11 ansible_ssh_common_args='-o StrictHostKeyChecking=no'
[db_servers]
192.168.100.12 ansible_ssh_common_args='-o StrictHostKeyChecking=no'
192.168.100.13 ansible_ssh_common_args='-o StrictHostKeyChecking=no'
```

1. 指纹解决之后会出现如下报错：

因为我们并没有指定用户名和密码，所以`SSH`无法正常连接。

```bash
[root@openEuler ~]# ansible all -m ping
192.168.100.10 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: \nAuthorized users only. All activities may be monitored and reported.\nroot@192.168.100.10: Permission denied (publickey,gssapi-keyex,gssapi-with-mic,password).",
    "unreachable": true
}
192.168.100.11 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: \nAuthorized users only. All activities may be monitored and reported.\nroot@192.168.100.11: Permission denied (publickey,gssapi-keyex,gssapi-with-mic,password).",
    "unreachable": true
}
192.168.100.12 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: Warning: Permanently added '192.168.100.12' (ED25519) to the list of known hosts.\r\n\nAuthorized users only. All activities may be monitored and reported.\nroot@192.168.100.12: Permission denied (publickey,gssapi-keyex,gssapi-with-mic,password).",
    "unreachable": true
}
192.168.100.13 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: Warning: Permanently added '192.168.100.13' (ED25519) to the list of known hosts.\r\n\nAuthorized users only. All activities may be monitored and reported.\nroot@192.168.100.13: Permission denied (publickey,gssapi-keyex,gssapi-with-mic,password).",
    "unreachable": true
}
```

​	解决方法（1）：

- - 命令行直接指定密码（临时使用），`-k`参数会让`Ansible`交互式提示输入密码

```bash
ansible all -m ping -k
```

​	解决方法（2）：

- - 在主机清单中通过变量配置密码

```bash
[web_servers]
192.168.100.10 ansible_user=root ansible_password=Huawei@123
192.168.100.11 ansible_user=root ansible_password=Huawei@123
[db_servers]
192.168.100.12 ansible_user=root ansible_password=Huawei@123
192.168.100.13 ansible_user=root ansible_password=Huawei@123
```

1. 密码问题解决后会出现如下提示：

```bash
[WARNING]: Platform linux on host 192.168.100.10 is using the discovered Python
interpreter at /usr/bin/python3, but future installation of another Python interpreter
could change this. See
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for
more information.

这个警告（WARNING）表明 Ansible 在目标主机 192.168.100.10 上自动发现了 Python 解释器（/usr/bin/python3），
但未来如果系统 Python 环境发生变化（例如安装了其他版本的 Python），可能会导致 Ansible 执行失败。
```

Ansible 模块依赖 Python 运行，默认会通过以下方式**自动探测**目标主机的 Python 路径：尝试 `python`、`python3`、`/usr/bin/python` 等常见路径。

解决方法（1）：在清单中显式指定 Python 解释器

```bash
# 静态清单文件（INI 格式）
[web_servers]
192.168.100.10 ansible_python_interpreter=/usr/bin/python3
```

​	解决方法（2）：全局配置（ansible.cfg）

```bash
[defaults]
interpreter_python = /usr/bin/python3
```

​	解决方法 （3）：完全禁用警告

```bash
[defaults]
interpreter_python = auto_legacy_silent
```

1. 所有问题解决后，便是如下正确结果：

```bash
[root@openEuler ~]# ansible all -m ping
192.168.100.10 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.12 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.11 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.13 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

##### 范例（2）：

由于`ansible`每次执行命令时都需要`SSH`连接到目标主机，而传统配置用户名和密码的方式太过繁琐，所以并不推荐。

推荐使用公钥认证（免密认证）的方式进行连接，如下：

1. 配置免密登录

```bash
### 在控制节点上生成密钥对
ssh-keygen -t rsa

### 将公钥复制到目标主机，需要输入ssh密码
ssh-copy-id  root@192.168.100.10

### 验证免密登录是否正常，如果直接登录成功（无需密码），说明配置正确
ssh root@192.168.100.10
```

1. 测试`ansible`免密连接

```bash
vim /etc/ansible/hosts
[web_servers]
192.168.0.10
192.168.0.11
[db_servers]
192.168.0.12
192.168.0.13

ansible all -m ping
```

##### 嵌套组（父子组）

在 Ansible 中，可以通过 **父子组（嵌套组）** 对主机进行分层管理，实现变量继承和批量操作。**嵌套组可以嵌套很多个层级。**

**父组的变量会自动传递给子组，而子组可以覆盖父组的变量（优先级更高）。**

在清单文件中，用`:children`定义父组，用普通组名作为子组。

```bash
[root@openEuler ~]# vim /etc/ansible/hosts
[web_servers]
192.168.100.10
192.168.100.11
[db_servers]
192.168.100.12
192.168.100.13
[production:children]
web_servers
db_servers

[root@openEuler ~]# ansible production -m ping
192.168.100.12 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.13 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.11 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.10 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

**查看当前组的嵌套关系：**

```bash
[root@openEuler ~]# ansible-inventory --graph
@all:
  |--@production:
  |  |--@db_servers:
  |  |  |--192.168.100.12
  |  |  |--192.168.100.13
  |  |--@web_servers:
  |  |  |--192.168.100.10
  |  |  |--192.168.100.11
  |--@ungrouped:
```

##### 定义主机范围

在主机清单中可以通过 **数字范围**、**字母范围** 或 **通配符** 批量定义主机，避免逐个列出 IP/主机名。

1. **数字范围（适用于 IP 或有序主机名）**

```bash
### 语法
[组名]
主机名前缀[开始:结束:步长]   # 步长可省略（默认为1）

### 示例
[web_servers]
192.168.100.[10:14:2]  # 等效于 web-1, web-2, web-3
192.168.100.10
192.168.100.12
192.168.100.14
[db_servers]
192.168.100.[13:14]  # 生成 db-1, db-3, db-5
```

1. **字母范围（适用于有序主机名）**

```bash
[log_servers]
log-[a:d]  # 生成 log-a, log-b, log-c, log-d
```

1. **通配符匹配（模糊匹配主机名）**

```bash
[all_servers]
*.example.com          # 匹配所有以 .example.com 结尾的主机
server-*.mydomain.org  # 匹配 server-01.mydomain.org, server-02.mydomain.org 等
```

##### 主机清单管理

当主机数量庞大（数百/数千台）且环境复杂（混合云、多团队协作）时，可通过以下目录结构和多清单策略实现高效管理：

1. 传递多个主机清单

可以通过命令行传递多个清单参数，或者配置 `ANSIBLE_INVENTORY`，来同时定位多个主机清单。

- 编辑主机清单：

```bash
[root@openEuler ~]# cat web_servers
[web_servers]
192.168.100.10
192.168.100.11
[root@openEuler ~]# cat db_servers
[db_servers]
192.168.100.12
192.168.100.13
```

- 指定多个主机清单

```bash
[root@openEuler ~]# ansible all -m ping -i db_servers -i web_servers
192.168.100.10 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.11 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.12 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.13 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

1. 在目录中存放主机清单

可以将多个主机清单整合到一个目录中。最简单的形式是使用包含多个文件的目录，而不是单个清单文件。当单个文件变得太长时，维护起来会变得困难。如果你有多个团队和多个自动化项目，为每个团队或项目创建一个清单文件可以让每个人轻松找到对他们重要的 host 和组。

- 创建目录存放主机清单

```bash
[root@openEuler ~]# mkdir /opt/inventroy
[root@openEuler ~]# mv db_servers /opt/inventroy/
[root@openEuler ~]# mv web_servers /opt/inventroy/
```

- 指定目录

```bash
[root@openEuler ~]# ansible all -m ping -i /opt/inventroy
192.168.100.12 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.11 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.13 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.10 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

- 可以直接在`/etc/ansible/ansible.cfg`指定主机清单目录

```bash
# ansible.cfg
[defaults]
# 指定清单目录（可以是绝对路径或相对路径）
inventory = /opt/inventroy

ansible --version	#检查当前配置是否生效
```

1. 主机清单加载顺序

Ansible 会按照文件名以 ASCII 顺序加载清单源。

如果你在一个文件或目录中定义了父组，在其他文件或目录中定义了子组，则必须先加载定义子组的文件。如果先加载父组，则会报错：

```bash
[root@openEuler inventroy]# cat a
[test:children]
web_servers
[root@openEuler inventroy]# cat b
[web_servers]
192.168.100.10
192.168.100.11
[root@openEuler inventroy]# ansible all -m ping -i /opt/inventroy
[WARNING]:  * Failed to parse /opt/inventroy/a with yaml plugin: We were unable to read
either as JSON nor YAML, these are the errors we got from each: JSON: Expecting value:
line 1 column 2 (char 1)  Syntax Error while loading YAML.   did not find expected
<document start>  The error appears to be in '/opt/inventroy/a': line 2, column 1, but
may be elsewhere in the file depending on the exact syntax problem.  The offending line
appears to be:  [test:children] web_servers ^ here
[WARNING]:  * Failed to parse /opt/inventroy/a with ini plugin: /opt/inventroy/a:2:
Section [test:children] includes undefined group: web_servers
[WARNING]: Unable to parse /opt/inventroy/a as an inventory source
192.168.100.10 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.11 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

为了避免这个问题，可以通过向文件添加前缀来控制加载顺序：

```bash
[root@openEuler inventroy]# mv a 02_a
[root@openEuler inventroy]# mv b 01_b
[root@openEuler inventroy]# ansible all -m ping -i /opt/inventroy
192.168.100.10 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.11 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
inventory/
  01-openstack.yml          # configure inventory plugin to get hosts from OpenStack cloud
  02-dynamic-inventory.py   # add additional hosts with dynamic inventory script
  03-on-prem                # add static hosts and groups
  04-groups-of-groups       # add parent groups
```

##### 变量

变量是 Ansible 自动化中存储动态值的核心机制，用于实现配置灵活性、环境适配和代码复用。我们可以直接将变量添加到主机清单文件中的`host`和组中。

这里只介绍将变量写在主机清单中的方法，不介绍其他方法及变量优先级。

###### 常见的变量

**连接控制变量**

| 变量名                         | 作用                    | 示例值              |
| ------------------------------ | ----------------------- | ------------------- |
| `ansible_host`                 | 覆盖实际连接的主机名/IP | `192.168.1.10`      |
| `ansible_port`                 | 指定非标准SSH端口       | `2222`              |
| `ansible_user`                 | 登录用户名              | `ubuntu`            |
| `ansible_ssh_private_key_file` | 指定SSH私钥路径         | `~/.ssh/deploy.key` |
| `ansible_password`             | SSH密码（不推荐明文）   | `P@ssw0rd`          |
| `ansible_become`               | 是否提权                | `true`              |
| `ansible_become_user`          | 提权目标用户            | `root`              |

**基础设施变量**

| 变量名            | 作用             | 示例值               |
| ----------------- | ---------------- | -------------------- |
| `http_port`       | 应用服务端口     | `8080`               |
| `db_host`         | 数据库服务器地址 | `db01.example.com`   |
| `max_connections` | 服务最大连接数   | `1000`               |
| `data_dir`        | 数据存储路径     | `/opt/data`          |
| `cluster_nodes`   | 集群节点列表     | `["node1", "node2"]` |

**命名规范**

- 使用小写+下划线命名法（如 `max_retries`）

**文档注释**  

```properties
[web_servers:vars]
# 生产环境Nginx配置
nginx_worker_processes=4  # 根据CPU核心数调整
```

**范例（1）：**

将`192.168.100.12`的`ssh`修改为`2222`，通过在主机清单的`host`增加`ansible_port`使其成功连接。

```bash
### 修改192.168.100.12的SSH端口
vim /etc/ssh/sshd_config
  Port 2222
setenforce 0
systemctl restart sshd
systemctl stop firewalld

### 在主机清单host添加变量
[root@openEuler ~]# vim /etc/ansible/hosts
  [web_servers]
  192.168.100.10
  192.168.100.11
  [db_servers]
  192.168.100.12 ansible_port=2222
  192.168.100.13

### 测试
[root@openEuler ~]# ansible all -m ping
192.168.100.10 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.12 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.11 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.13 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

**范例（2）：**

将`192.168.100.12`的`root`密码修改为`123`，指定`host`密码变量为`123`，组的密码变量为`Huawei@123`，查看最终以哪个为准：

```bash
### 修改密码
passwd

### 修改主机清单
[root@openEuler ~]# vim /etc/ansible/hosts
  [web_servers]
  192.168.100.10
  192.168.100.11
  [db_servers]
  192.168.100.12 ansible_port=2222 ansible_password=123
  192.168.100.13
  [db_servers:vars]
  ansible_password=Huawei@123

### 测试
[root@openEuler ~]# ansible all -m ping
192.168.100.12 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.10 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.13 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.11 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

- 结论：当`host`和主机组指定相同变量，且内容不一致时，以`host`变量为实际值。

**范例（3）：**

在范例（2）的基础上定义父组的密码变量，查看最终以哪个变量为实际值：

```bash
[root@openEuler ~]# vim /etc/ansible/hosts
  [web_servers]
  192.168.100.10
  192.168.100.11
  [db_servers]
  192.168.100.12 ansible_port=2222 ansible_password=123
  192.168.100.13
  [db_servers:vars]
  ansible_password=Huawei@123
  [production:children]
  web_servers
  db_servers
  [production:vars]
  ansible_password=12345

  
[root@openEuler ~]# ansible all -m ping
192.168.100.12 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.10 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.13 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.100.11 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

- 结论：当定义了不同级别的变量时，优先级为：主机变量>主机组变量>父组变量

### 三、Ansible 进阶

#### Ansible 常用模块

官网内置模块：`https://docs.ansible.com/ansible/latest/collections/ansible/builtin/index.html#plugins-in-ansible-builtin`

##### file 模块

`file`模块是`ansible`中用于管理文件和目录的核心模块，它可以创建文件、目录、符号链接、设置权限和属性等。

**常用参数**

| **参数**      | **说明**                                                     | **示例**                  |
| ------------- | ------------------------------------------------------------ | ------------------------- |
| `**path**`    | **文件/目录路径（别名：**`**dest**`**,** `**name**`**）**    | `**path: /etc/foo.conf**` |
| `**state**`   | **状态：**`**file**`**,** `**directory**`**,** `**link**`**,** `**hard**`**,** `**touch**`**,** `**absent**` | `**state: directory**`    |
| `**mode**`    | **权限（如 0644）**                                          | `**mode: '0644'**`        |
| `**owner**`   | **文件所有者**                                               | `**owner: root**`         |
| `**group**`   | **文件所属组**                                               | `**group: www-data**`     |
| `**recurse**` | **递归设置目录权限**                                         | `**recurse: yes**`        |
| `**src**`     | **链接的源文件（当**`**state=link**`**或**`**hard**`**时）** | `**src: /etc/foo.conf**`  |
| `**force**`   | **强制创建链接（当目标存在时）**                             | `**force: yes**`          |

- `touch`：创建文件、更新时间戳。
- `file`：修改文件属性

**示例：**

1. 创建目录

```bash
ansible all -m file -a "path=/opt/dir state=directory"
```

1. 创建文件

```bash
ansible all -m file -a "path=/opt/dir/file1.txt state=touch"
```

1. 创建符号链接

```bash
ansible all -m file -a "src=/etc/hosts dest=/opt/dir/hosts_link state=link"
```

1. 删除文件或目录

```bash
### 删除目录
ansible all -m file -a "path=/opt/dir state=absent"

### 删除文件
ansible all -m file -a "path=/opt/dir/file1.txt state=absent"
```

1. 修改文件属性

```bash
### 修改文件权限
ansible all -m file -a "path=/opt/dir/file1.txt mode=0640 owner=root group=root"

### 递归修改目录权限
ansible all -m file -a "path=/opt/dir mode=0640 owner=root group=root recurse=yes"
```

##### user 模块

Ansible 的 `user` 模块用于管理系统用户账户，包括创建、修改和删除用户，以及管理用户属性如密码、组、家目录等。

**常用参数**

| 参数               | 说明                                   | 示例                        |
| ------------------ | -------------------------------------- | --------------------------- |
| `name`             | 用户名（必需）                         | `name: testuser`            |
| `state`            | 用户状态：present(存在)/absent(不存在) | `state: present`            |
| `uid`              | 用户 UID                               | `uid: 1001`                 |
| `group`            | 用户主组                               | `group: developers`         |
| `groups`           | 用户附加组列表                         | `groups: wheel,devops`      |
| `home`             | 用户家目录路径                         | `home: /home/testuser`      |
| `shell`            | 用户默认 shell                         | `shell: /bin/bash`          |
| `comment`          | 用户描述信息                           | `comment: "Test User"`      |
| `password`         | 用户密码（加密后的）                   | `password: $6$salt$hash`    |
| `generate_ssh_key` | 是否生成 SSH 密钥                      | `generate_ssh_key: yes`     |
| `ssh_key_type`     | SSH 密钥类型                           | `ssh_key_type: rsa`         |
| `ssh_key_file`     | SSH 密钥文件路径                       | `ssh_key_file: .ssh/id_rsa` |
| `system`           | 是否为系统用户                         | `system: yes`               |
| `create_home`      | 是否创建家目录                         | `create_home: no`           |

**范例（1）：创建用户**

```bash
ansible all -m user -a "name=testuser state=present shell=/sbin/nologin group=test groups=test1 home=/home/test create_home=yes"
```

**范例（2）：删除用户**

```bash
ansible all -m user -a "name=testuser state=absent remove=yes"
```

##### group 模块

`group` 模块是 Ansible 中用于管理系统用户组的核心模块，可以创建、修改和删除用户组。

**主要参数**

| 参数     | 说明                   | 示例值       |
| -------- | ---------------------- | ------------ |
| `name`   | 组名（必需）           | `developers` |
| `state`  | 组状态：present/absent | `present`    |
| `gid`    | 指定组 GID             | `1001`       |
| `system` | 是否为系统组           | `yes`        |

**范例（1）： 创建基本用户组**

```bash
ansible all -m group -a "name=developers"
```

**范例（2）：创建指定 GID 的组**

```bash
ansible webservers -m group -a "name=deploy gid=1042"
```

**范例（3）：创建系统组**

```bash
ansible db_servers -m group -a "name=dbadmin system=yes"
```

**范例（4）：删除组**

```bash
ansible old_servers -m group -a "name=legacy state=absent"
```

**范例（5）：修改组 GID**

```bash
ansible app_servers -m group -a "name=appusers gid=1500"
```

##### yum 模块

`yum` 模块是 Ansible 中用于管理 RHEL/CentOS/Fedora/openEuler 等基于 RPM 的 Linux 系统中软件包的核心模块。

**主要参数**

| 参数            | 说明                        | 示例值                  |
| --------------- | --------------------------- | ----------------------- |
| `name`          | 包名/包组名/URL             | `httpd`, `@development` |
| `state`         | 状态：present/latest/absent | `latest`                |
| `enablerepo`    | 临时启用仓库                | `epel`                  |
| `disablerepo`   | 临时禁用仓库                | `updates`               |
| `exclude`       | 排除的包                    | `kernel*`               |
| `update_cache`  | 更新元数据缓存              | `yes`                   |
| `list`          | 列出包（不执行操作）        | `httpd`                 |
| `security`      | 仅安全更新                  | `yes`                   |
| `download_only` | 仅下载不安装                | `yes`                   |

范例（1）：安装单个软件包

```bash
ansible webservers -m yum -a "name=httpd state=present"
```

范例 （2）：安装最新版本

```bash
ansible all -m yum -a "name=nginx state=latest"
```

范例（3）：安装多个软件包

```bash
ansible app_servers -m yum -a "name=vim-enhanced,git,tmux state=present"
```

范例（4）：删除软件包

```bash
ansible old_servers -m yum -a "name=telnet state=absent"
```

范例（5）：使用特定仓库安装

```bash
ansible all -m yum -a "name=http enablerepo=epel state=present"
```

范例（6）：更新所有软件包

```bash
ansible production -m yum -a "name=* state=latest"
```

范例（7）：仅安全更新

```bash
ansible critical -m yum -a "security=yes state=latest"
```

范例（8）：安装包组

```bash
ansible dev_hosts -m yum -a "name='@development' state=present"
```

范例（9）：下载但不安装

```bash
ansible all -m yum -a "name=ansible download_only=yes"
```

范例（10）：从URL安装RPM

```bash
ansible all -m yum -a "name=https://example.com/packages/custom.rpm state=present" -b
```

范例（11）：排除特定包更新

```bash
ansible all -m yum -a "name=* state=latest exclude=kernel*"
```

范例（12）：清理YUM缓存

```bash
ansible all -m yum -a "clean=all"
```

范例（13）：列出可用更新

```bash
ansible all -m yum -a "list=updates"
```

范例（14）：检查包是否安装

```bash
ansible all -m yum -a "list=httpd"
```

范例（15）：验证命令

```bash
# 检查包是否安装
ansible all -m shell -a "rpm -q httpd" -b

# 检查版本
ansible all -m shell -a "nginx -v" -b
```

##### copy 模块

`copy` 模块是 Ansible 中用于文件传输的核心模块，可以将本地文件复制到远程主机，或直接在远程主机上创建新文件。

**主要参数**

| 参数       | 说明               | 示例值                        |
| ---------- | ------------------ | ----------------------------- |
| `src`      | 源文件路径（本地） | `/tmp/file.conf`              |
| `dest`     | 目标路径（远程）   | `/etc/file.conf`              |
| `content`  | 直接写入的内容     | `"Hello World"`               |
| `owner`    | 文件所有者         | `root`                        |
| `group`    | 文件所属组         | `wheel`                       |
| `mode`     | 文件权限           | `0644`                        |
| `backup`   | 是否备份原文件     | `yes`                         |
| `force`    | 是否强制覆盖       | `no`                          |
| `validate` | 更新前验证命令     | `"/usr/sbin/apachectl -t %s"` |

范例（1）：基本文件复制

```bash
ansible webservers -m copy -a "src=/tmp/app.conf dest=/etc/app.conf"
```

范例（2）：设置文件权限和所有者

```bash
ansible all -m copy -a "src=/tmp/script.sh dest=/usr/local/bin/script.sh owner=root group=root mode=0755"
```

范例（3）：直接创建文件内容

```bash
ansible db_servers -m copy -a "content='DB_HOST=127.0.0.1' dest=/etc/db.conf"
```

范例（4）：复制并备份原文件

```bash
ansible production -m copy -a "src=/tmp/nginx.conf dest=/etc/nginx/nginx.conf backup=yes"
```

范例（5）：在单个主机上复制文件

```bash
ansible hostA -m copy -a "src=/path/to/source dest=/path/to/dest remote_src=yes"
```

范例（6）：验证命令

```bash
# 检查文件是否存在
ansible all -m shell -a "ls -l /etc/app.conf" -b

# 检查文件内容
ansible all -m shell -a "cat /etc/motd" -b

# 检查备份文件
ansible all -m shell -a "ls -l /etc/nginx/nginx.conf.*" -b
```

##### systmd 模块

`systemd` 模块是 Ansible 中用于管理系统服务的核心模块，专门用于基于 systemd 的 Linux 系统。

**主要参数**

| 参数      | 说明                                         | 示例值    |
| --------- | -------------------------------------------- | --------- |
| `name`    | 服务名称（必需）                             | `nginx`   |
| `state`   | 服务状态：started/stopped/restarted/reloaded | `started` |
| `enabled` | 开机自启：yes/no                             | `yes`     |

范例（1）：启动服务

```bash
ansible webservers -m systemd -a "name=nginx state=started"
```

范例（2）： 停止服务

```bash
ansible all -m systemd -a "name=httpd state=stopped"
```

范例（3）： 重启服务

```bash
ansible app_servers -m systemd -a "name=mysqld state=restarted"
```

范例（4）：重载服务（不重启）

```bash
ansible load_balancers -m systemd -a "name=haproxy state=reloaded"
```

范例（5）：启用开机自启

```bash
ansible db_servers -m systemd -a "name=postgresql enabled=yes"
```

范例（6）：禁用开机自启

```bash
ansible legacy_servers -m systemd -a "name=tomcat enabled=no"
```

范例（7）：检查服务状态

```bash
ansible all -m systemd -a "name=sshd"
```

范例（8）：验证命令

```bash
# 检查服务状态
ansible all -m shell -a "systemctl is-active nginx"

# 检查是否启用
ansible all -m shell -a "systemctl is-enabled nginx"

# 查看详细状态
ansible all -m shell -a "systemctl status nginx --no-pager"
```

##### mount 模块

`mount` 模块是 Ansible 中用于管理文件系统挂载的核心模块，可以永久性配置 `/etc/fstab` 中的挂载项并控制当前挂载状态。

**主要参数**

| 参数     | 说明                                   | 示例值                              |
| -------- | -------------------------------------- | ----------------------------------- |
| `path`   | 挂载点路径（必需）                     | `/mnt/data`                         |
| `src`    | 要挂载的设备/资源                      | `/dev/sdb1` 或 `nfs-server:/export` |
| `fstype` | 文件系统类型                           | `ext4`, `nfs`, `xfs`                |
| `state`  | 状态：present/absent/mounted/unmounted | `mounted`                           |
| `opts`   | 挂载选项                               | `rw,noatime`                        |
| `dump`   | dump 备份标志                          | `0`                                 |
| `passno` | fsck 检查顺序                          | `2`                                 |
| `boot`   | 是否在启动时挂载                       | `yes`                               |

- `mounted`会挂载并写入 `fstab`
- `unmoted` 会卸载但不改变 `fstab`
- `present` 只写入 `fstab` 不执行挂载
- `absent` 删除 `fstab`，也取消挂载

范例（1）：挂载本地设备并永久生效

```bash
ansible all -m mount -a "path=/data src=/dev/sdb1 fstype=ext4 state=mounted opts=rw,noatime" -b
```

范例（2）：挂载 NFS 共享

```bash
ansible app_servers -m mount -a "path=/mnt/nfs src=nfs01:/data/share fstype=nfs opts=rw,hard,intr state=mounted" -b
```

范例（3）：卸载文件系统（保留 fstab 记录）

```bash
ansible all -m mount -a "path=/mnt/temp state=unmounted" -b
```

范例（4）：完全移除挂载配置

```bash
ansible old_servers -m mount -a "path=/mnt/legacy state=absent" -b
```

范例（5）：临时挂载（不写入 fstab）

```bash
ansible test_servers -m mount -a "path=/tmp/test src=/dev/sdc1 fstype=xfs state=mounted boot=no" -b
```

范例（6）：配置交换分区

```bash
ansible all -m mount -a "path=none src=/dev/sdb2 fstype=swap state=present" -b
```

范例（7）：修改现有挂载选项

```bash
ansible webservers -m mount -a "path=/var/www src=/dev/sdd1 fstype=ext4 opts=rw,noexec state=present" -b
```

范例（8）：检查挂载状态

```bash
ansible all -m mount -a "path=/mnt/data state=present" -b
```

范例（9）：挂载 CIFS/SMB 共享

```bash
ansible clients -m mount -a "path=/mnt/smb src=//fileserver/share fstype=cifs opts=username=user,password=pass,uid=1000 state=mounted" -b
```

范例（10）：验证命令

```bash
# 检查挂载点是否存在
ansible all -m shell -a "ls -ld /mnt/data"

# 检查当前挂载情况
ansible all -m shell -a "mount | grep /mnt/data"

# 检查 fstab 配置
ansible all -m shell -a "grep /mnt/data /etc/fstab"

# 检查挂载选项
ansible all -m shell -a "findmnt -n -o OPTIONS /mnt/data"
```

##### cron 模块

name 的作用是判断这个任务是否已经存在，以及更新覆盖。

`cron` 模块是 Ansible 中用于管理系统定时任务（cron jobs）的核心模块，可以创建、修改或删除 crontab 条目。

**主要参数**

| 参数           | 说明                                                    | 示例值               |
| -------------- | ------------------------------------------------------- | -------------------- |
| `name`         | 任务描述/注释（标识用）                                 | "备份数据库"         |
| `user`         | 任务所属用户                                            | "root"               |
| `job`          | 要执行的命令                                            | "/path/to/script.sh" |
| `minute`       | 分钟（0-59）                                            | "*/5"、"0,30"        |
| `hour`         | 小时（0-23）                                            | "3"、"*/2"           |
| `day`          | 日期（1-31）                                            | "*"、"15"            |
| `month`        | 月份（1-12）                                            | "*"、"1,4,7,10"      |
| `weekday`      | 星期几（0-6，0=周日）                                   | "*"、"1-5"           |
| `special_time` | 预设时间（annually/monthly/weekly/daily/hourly/reboot） | "daily"              |
| `state`        | 状态：present/absent                                    | "present"            |
| `disabled`     | 是否禁用任务                                            | "yes"                |
| `environment`  | 环境变量                                                | "PATH=/usr/bin:/bin" |
| `backup`       | 修改前是否备份原crontab                                 | "yes"                |

范例（1）：创建基本 cron 任务

```bash
ansible all -m cron -a 'name="日常备份" user=root job="/opt/scripts/backup.sh" minute=0 hour=2' -b
```

范例（2）： 使用预设时间（每天执行）

```bash
ansible webservers -m cron -a 'name="清理日志" job="/opt/scripts/clean_logs.sh" special_time=daily' -b
```

范例（3）：创建复杂时间任务

```bash
ansible db_servers -m cron -a 'name="数据库维护" minute=30 hour=3 day=15 month="*/2" weekday=1-5 job="/opt/db/maintenance.sh"' -b
```

范例（4）：为特定用户创建任务

```bash
ansible app_servers -m cron -a 'user=appuser name="应用监控" job="/home/appuser/monitor.sh" minute="*/10"' -b
```

范例（5）：禁用 cron 任务

```bash
ansible all -m cron -a 'name="日常备份" disabled=yes' -b
```

范例（6）：删除 cron 任务

```bash
ansible old_servers -m cron -a 'name="旧任务" state=absent' -b
```

范例（7）：带环境变量的任务

```bash
ansible all -m cron -a 'name="带环境变量的任务" job="/opt/scripts/env_test.sh" hour=1 environment="PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin"' -b
```

范例（8）：检查 cron 任务是否存在

```bash
ansible all -m cron -a 'name="日常备份" job="/opt/scripts/backup.sh" minute=0 hour=2' -b
```

范例（9）：验证命令

```bash
# 查看root用户的cron任务
ansible all -m shell -a 'crontab -l' -b

# 查看特定用户的cron任务
ansible all -m shell -a 'crontab -u appuser -l' -b

# 检查特定任务是否存在
ansible all -m shell -a 'crontab -l | grep "日常备份"' -b
```

#### Ansible Playbook

`Ansible PlayBook`是`Ansible`的核心组件之一，用于定义自动化任务。采用`YAML`格式编写，允许以声明式的方式描述服务器配置、应用部署、服务管理等操作。

`PlayBook`即剧本，类似于电影的剧本。一部电影由很多很多个不同的场景组成，类似于第一场戏、第二场戏。一场戏中有很多很多的组成：演员、背景、道具、特效、台词等等，而这一切最终都会由剧本编排，组成最终我们看到的电影。`PlayBook`也是同样的原理，可以将一个一个不同的任务进行编排，最终完成我们想要的效果。

##### Ansible Playbook 的基本结构

一个基本的`PlayBook`由以下内容组成：

- 目标主机（`hosts`）：定义在哪些机器上执行任务
- 变量（`vars`）：可选的变量
- 任务（`tasks`）：具体要执行的操作（调用模块）
- `handlers`：由任务触发的事件（若执行任务后状态发生改变，则执行`handlers`中定义的任务）

`PlayBook`示例：

```bash
- name: Install and start Nginx  # Play 的名称
  hosts: web_servers             # 目标主机组（在 inventory 中定义）
  tasks:
    - name: Install Nginx        # 任务1：安装 Nginx
      yum:
        name: nginx
        state: present
    - name: Start Nginx service  # 任务2：启动服务
      systemd:
        name: nginx
        state: started
        enabled: yes
```

对应的`ad-hoc`：

```bash
ansible web_servers -m yum -a "name=nginx state=present"
ansible web_servers -m systemd -a "name=nginx state=started enabled=yes"
```

**为什么每个任务要写一个**`**name**`**？**

- 我们可以通过指定`name`的方式控制整个`PlayBook`从哪里开始运行或只运行某个任务。

##### YAML 基础语法

- **缩进：**必须使用**空格**（不能使用 Tab），通常`2`个空格缩进（可以不是`2`个，但需要统一）
- **键值对：**`key: value`（冒号后必须有空格）
- **列表：**以`-`开头，表示多个项。类似于`Python`中的`list`
- **注释：**以`#`开头
- **文件的后缀：**`*.yaml`或`*.yml`

```bash
---
# 这是一个注释
name: "My Playbook"  # 键值对
tasks:               # 列表
  - task1
  - task2
```

**为什么**`**tasks**`**下的任务名称有**`**-**`**？**

因为`tasks`是一个列表，每个任务都是列表中的一项，所以需要用`-`开头。

**为什么其他没有**`**-**`**？**

```bash
- name: Play 1       # 这是一个 Play（列表项）
  hosts: web_servers # Play 的字典成员（键值对）
  become: yes        # Play 的字典成员
  tasks:             # Play 的字典成员（值是一个列表）
    - name: Task1    # tasks 列表的子项
```

##### 范例（1）：编写一个`Nginx`剧本

```bash
- name: 剧本名称
  hosts: 角色、演员表
  tasks: 剧本正文
  - name: 分镜（描述）
    yum: 主角
      name: 名字
      state: 动作
  - name: 分镜2
    service: 主角
      name: 名字
      state: 动作
```

**为什么模块这里和官方文档写的不一样呢？**

- 新版本的 ansible 模块分了很多个类别，所以新版的 `ansible playbook` 写模块的时候，写的很细。我们依旧可以使用旧版本的语法去写，也就是只写模块的名称。

##### 执行 PlayBook

```bash
ansible-playbook test.yaml
ansible-playbook -C test.yaml # -C=--check
```

##### 范例（2）：编写一个 NFS 剧本

- `NFS`服务端`PlayBook`

```bash
- name: nfs
  hosts: nfs_servers  # 在inventory文件中定义的主机组
  become: yes         # 使用root权限

  tasks:
    # 安装必要的软件包
    - name: 安装NFS服务端软件
      yum:
        name: nfs-utils
        state: present

    # 创建共享目录
    - name: 创建共享目录
      file:
        path: /data/share
        state: directory
        mode: '0777'

    # 配置NFS导出
    - name: 配置NFS导出
      lineinfile:
        path: /etc/exports
        line: "/data/share 192.168.100.0/24(rw,sync,no_root_squash)"
        state: present

    # 启动NFS服务
    - name: 启动NFS服务
      service:
        name: nfs-server
        state: started
        enabled: yes
```

- `NFS`客户端`PlayBook`

```bash
- name: 配置NFS客户端
  hosts: nfs_clients  # 在inventory文件中定义的主机组
  become: yes         # 使用root权限

  tasks:
    # 安装NFS客户端软件
    - name: 安装NFS客户端软件
      yum:
        name: nfs-utils
        state: present

    # 创建挂载点目录
    - name: 创建挂载点目录
      file:
        path: /mnt/nfs_share
        state: directory
        mode: '0777'

    # 挂载NFS共享
    - name: 挂载NFS共享
      mount:
        path: /mnt/nfs_share
        src: "192.168.100.100:/data/share"  # 替换为实际的NFS服务器IP
        fstype: nfs
        opts: "rw,sync"
        state: mounted

    # 确保开机自动挂载
    - name: 添加到fstab实现开机自动挂载
      lineinfile:
        path: /etc/fstab
        line: "192.168.100.100:/data/share /mnt/nfs_share nfs rw,sync 0 0"
        state: present
```

##### PlayBook 的简便写法

```bash
-name: 06-start
  systemd: name=fs state=started enabled=true
```

##### 循环

Ansible 提供了多种循环机制来简化重复性任务的操作。循环可以让你对一组数据项执行相同的任务，而不需要为每个项单独编写任务。

例如，拷贝文件和创建目录等任务。当需要使用`PlayBook`多次创建文件或目录时，我们需要重复的书写。如下：

```bash
- name: 创建多个文件（不使用循环）
  hosts: localhost
  tasks:
    - name: 创建文件1
      file:
        path: /tmp/file1.txt
        state: touch
        mode: '0644'
    
    - name: 创建文件2
      file:
        path: /tmp/file2.txt
        state: touch
        mode: '0777'
    
    - name: 创建文件3
      file:
        path: /tmp/file3.txt
        state: touch
        mode: '0644'
    
    - name: 创建文件4
      file:
        path: /tmp/file4.txt
        state: touch
        mode: '0644'
    
    - name: 创建文件5
      file:
        path: /tmp/file5.txt
        state: touch
        mode: '0644'
```

使用循环的方式书写，整体的框架只需要写一次，如下：

```bash
- name: 创建多个文件
  hosts: localhost
  tasks:
    - name: 创建文件1
      file:
        path: "{{ item }}"
        state: touch
      loop:
        - /opt/test1.txt
        - /opt/test2.txt
```

具体格式解析：

```bash
- name: 任务描述
  module_name:
    参数1: "{{ item }}"  # 循环变量
    参数2: 值
  loop:
    - 值1
    - 值2
    - 值3
```

所以，循环是帮助我们节省重复书写的内容，实现方式接近于变量。需要变动的地方就用变量代替，不变的地方就写死。

##### 多循环

很多时候一个任务中，我们有许多需要变动的值，而这个任务又需要重复的执行多次。这个时候用单循环无法解决我们的需求，就需要使用多循环了。

例如，需要创建多个文件，且每个文件的权限不一致，我们就可以使用多循环的方式，将`path`和`mode`的值用循环变量代替。如下：

```bash
- name: create
    file:
      path: "{{ item.path }}"
      state: touch
      mode: "{{ item.mode }}"
    loop:
      - { path: '/opt/file1.txt', mode: '0644' }
      - { path: '/opt/file2.txt', mode: '0600' }
```

有一个场景如果需要多次执行并简化`playbook`内容必须要用到多循环：`COPY`

**请仿照上述例子，写出使用多循环多次复制文件的例子。**

##### 变量

变量是存储和引用数据的重要方式，它们使得 Playbook 更加灵活和可重用。

1. 当某些值可能会被经常用到时，就可以将他定义成一个变量。自定义
2. ansible 内置了很多变量，可以直接拿来用

**自定义变量**

当某些值可能会被经常用到时，就可以将其定义成一个变量。

假如，我们在复制文件时，有巨多的文件都存储在`/opt/xxx/xxx/xxx/xxx`下，此时就可以将这个路径存储为一个变量，后续使用时直接调用这个变量即可。

另外，若我们需要大量修改这个目录的路径时，只需要修改变量的值即可，不需要再修改每个内容的具体值，既方便也不容易出错。

注意，写在`playbook`中的变量属于局部变量，无法被其他`playbook`调用。

**示例：**

```bash
---
- name: 使用变量管理文件路径示例
  hosts: all
  vars:
    # 定义基础路径变量
    source_dir: "/root/apps/config_files/production"
    destination_dir: "/etc/application/config"
    
    # 可以定义子路径变量
    log_config_path: "{{ source_dir }}/logging"
    db_config_path: "{{ source_dir }}/database"
    
  tasks:
    - name: 创建目录
      file:
        path: "{{ destination_dir }}"
        state: directory
        recurse: yes
        mode: '0755'
      
    - name: 复制日志配置文件
      copy:
        src: "{{ log_config_path }}/log4j.properties"
        dest: "{{ destination_dir }}/log4j.properties"
        remote_src: no  # 如果源文件在控制节点上
        
    - name: 复制数据库配置文件
      copy:
        src: "{{ db_config_path }}/db.conf"
        dest: "{{ destination_dir }}/db.conf"
        
    - name: 复制所有配置文件（使用通配符）
      copy:
        src: "{{ source_dir }}/*.conf"
        dest: "{{ destination_dir }}/"
```

##### 主机清单存储变量

当我们需要变量跨`playbook`调用时，可以将变量定义在主机清单文件中，但此方法的前提是调用该主机或主机组。

```bash
[webservers]
web1.example.com source_dir="/root/apps/config_files/production"
[webservers:vars]
ntp_server=ntp.example.com
proxy=proxy.example.com
timezone=UTC
```

##### 内置变量

`Ansible`提供了很多内置变量，这些变量由`Ansible`自动设置并提供系统信息、执行上下文等重要数据。

当我们运行`PlayBook`时，`Ansible`自动就会获取目标主机的基本信息，这些基本信息我们可以通过`ansible web -m setup >> vars.txt`的方式获取到。这里面记录的就是内置变量。

获取之后，我们就可以通过`PlayBook`的方式调用内置变量，实现我们的目的。例如，使所有目标主机`echo`自己的`IP`地址信息。

##### Facts

在`ansible`执行时，默认会有一个任务先运行：`Gathering Fact`

```bash
TASK [Gathering Facts] ****************************************
ok: [192.168.xxx.xxx]
```

这并不是我们在`playbook`中定义的任务，这是默认执行的任务。

`ansible facts`是`ansible`在被纳管主机上自动检测的变量。`facts`组件是`ansible`用于采集被纳管主机信息的一个功能，采集的信息包括`IP`地址、操作系统、以太网设备、`mac`地址、硬件信息等相关数据。

那么，采集这些信息有什么用呢？很多时候我们需要根据远程主机的信息作为判断条件操作。例如：根据被纳管主机的操作系统版本，安装不同的软件包。或者获取每台设备上的内存剩余等。

`ansible`为我们提供了`setup`模块，专门获取被纳管主机的所有`facts`信息。`setup`模块获取的整个`facts`信息被包装在一个`JSON`格式的数据结构中，`ansible_facts`是最外层的值。我们可以通过`ansible Ad-Hoc`进行查看。

```bash
ansible localhost -m setup >> facts.txt
```

你可以进行过滤筛选出你想要的信息：

```bash
ansible localhost -m setup -a 'filter=ansible_fqdn'
```

`facts`收集到的信息，会被存储为变量，可以称为事实变量，这些变量有新旧两种书写方式：

![img](https://cdn.nlark.com/yuque/0/2025/png/42713143/1743954575783-6e03a5ca-f0c5-4563-b3ec-dfbe9498b702.png)

##### 条件判断

`ansible`中的条件判断通过`when`实现，允许根据变量、`facts`或任务结果来控制任务执行。

**范例（1）**

```bash
tasks:
  - name: Shutdown Debian systems
    command: /sbin/shutdown -t now
    when: ansible_facts['os_family'] == "Debian"
```

- 该任务表示，当目标主机的系统是`Debian`时才会执行该任务。

**逻辑运算符**

`ansible`的条件判断中支持`and、or`及括号组合条件

```bash
when: >
  (ansible_distribution == "Ubuntu" and ansible_distribution_major_version == "22.04") 
  or (ansible_distribution == "CentOS" and ansible_distribution_major_version == "8")
```

##### Handlers 服务状态

Handlers 是 Ansible 中一种特殊的任务类型，用于在 playbook 执行过程中管理服务重启和配置变更后的操作。

**基本概念**

- 只在被通知(notify)时才会执行的任务
- 通常用于服务重启、重新加载配置等操作
- 在 play 的所有普通任务执行完毕后才会运行
- 即使被多次通知，也只会执行一次

**举例：**

如下，是`NFS`服务配置的其中一个任务，这个任务的作用是启动`NFS`服务。假设我现在将`NFS`的配置文件改动并重新执行这个`PlayBook`上传到目标主机上，这个配置会生效么？

很显然不会，因为这里写的是`started`，而不是`restarted`。那是不是代表，我这要把这里的`started`替换成`restarted`就可以了呢？不行，因为`ansible`的特点是每一次执行它会帮助我们查询状态，如果`restarted`不就代表状态被改变了吗，那么回显一定是黄色的，这不方便我们判断`playbook`执行的结果。

所以，我们应该在这里做`Handlers`，帮助我们去检测运行状态。

```bash
    - name: 启动NFS服务
      service:
        name: nfs-server
        state: started
        enabled: yes
```

我们的需求是：

- 当第一次进行`NFS`服务安装时，帮助我们启动服务
- 当配置文件没有发生变化时，不做任何动作
- 当配置文件发生变化时，重启服务

下面这个`playbook`就是我们修改完成的，`notify`表示当此任务的状态发生改变后，需要执行`handlers`中的任务。注意：

1. `handlers`的`name`必须和`notify`定义的内容一致，否则无法识别到
2. `handlers`中的任务会在你所有预定义的任务执行完毕，最后再执行

```bash
- name: nfs
  hosts: nfs_servers  # 在inventory文件中定义的主机组
  become: yes         # 使用root权限

  tasks:
    # 安装必要的软件包
    - name: 安装NFS服务端软件
      yum:
        name: nfs-utils
        state: present

    # 创建共享目录
    - name: 创建共享目录
      file:
        path: /data/share
        state: directory
        mode: '0777'

    # 配置NFS导出
    - name: 上传NFS配置文件
      copy:
        src: files/exports  # 本地文件路径: playbook/files/exports
        dest: /etc/exports
      notify: restart NFS

    # 启动NFS服务
    - name: start NFS
      systemd:
        name: nfs-server
        state: started
        enabled: yes
  handlers:
    - name: restart NFS
      systemd:
        name: nfs-server
        state: restarted
```

##### 指定任务执行顺序

在`ansible`中，有几种方式可以控制`playbook`从特定任务开始执行，而不是从头开始运行整个`playbook`。

**tasks**

通过在执行`playbook`时添加`--start-at-stack`参数，指定从哪个任务开始依次运行：

```bash
ansible-playbook playbook.yml --start-at-task="任务描述"
```

- 这里的`“任务描述”`就是我们在`playbook`当中定义的任务名

通过添加`--list-tasks`参数可获取`playbook`中所有的`tasks`：

```bash
ansible-playbook --list-tasks playbook.yaml
```

**选择 tag**

`tasks`没有那么的灵活，只能控制从哪个`tasks`开始运行。无法实现只运行某个任务、或跳过特定的任务等目的。

可以通过为每个任务添加标签，然后实现只运行特定标签的任务，或跳过特定标签的任务。

`tags`需要与任务的名称对齐，如下：

```bash
tasks:
  - name: 安装软件包
    yum:
      name: nginx
      state: present
    tags: install

  - name: 配置服务
    template:
      src: nginx.conf.j2
      dest: /etc/nginx/nginx.conf
    tags: config
&&
ansible-playbook playbook.yml --tags(-t) "config,install"
ansible-playbook playbook.yml --skip-tag=config,install
```

但是，执行时一定会按照`tag`在`playbook`中的顺序执行，即使你故意写反，它也一定按照任务顺序执行。

**运行检查规范**

1. 检查剧本拼写规范

```bash
ansible-playbook your_playbook.yaml --syntax-check
```

1. 检查这个任务执行的主机对象

```bash
ansible-playbook your_playbook.yaml --list-hosts
```

1. 检查这个剧本需要执行哪些任务

```bash
ansible-playbook your_playbook.yaml --list-tasks
ansible-playbook your_playbook.yaml --list-tags
```

1. 模拟执行剧本

```bash
ansible-playbook your_playbook.yaml --check(-C)
```

1. 真正执行剧本

```bash
ansible-playbook your_playbook.yaml
```

#### 角色

`ansible role`是一种组织`playbook`的方式，它将相关的任务、变量、配置文件、模板等组织到一个预定义的文件结构中。使用`roles`可以使`playbook`更加模块化、可重用和易于管理。

`**playbook**`**存在的问题**

1. 配置文件乱放
2. 功能重复，太多冗余
3. 所有的任务写在同一个文件里，容易修改错误，篇幅太长，没有按照功能拆分

`**Roles**`**的好处**

1. 模块化、代码复用

- 将相关任务、变量、文件和模板打包成独立单元
- 一次开发，多次使用

1. 组织结构清晰
2. 协作与维护

`**Role**`**的基本结构**

```bash
role_name/	#目录
├── defaults/          # 默认变量 (最低优先级)
│   └── main.yml
├── vars/             # 其他变量 (较高优先级)
│   └── main.yml
├── tasks/            # 主任务列表
│   └── main.yml
├── handlers/         # 处理器
│   └── main.yml
├── files/            # 静态文件
├── templates/        # Jinja2 模板
├── meta/             # 角色依赖
│   └── main.yml
└── tests/            # 测试用例
```

**使用**`**roles**`**实现**`**NFS**`

1. 构建`roles`目录
2. 编辑`tasks/main.yaml`

```bash
# tasks/main.yml
- name: 01_install_nfs
  yum:
    name: nfs-utils
    state: present

- name: 02_create_directory
  file:
    path: /data
    state: directory
    mode: "0777"

- name: 03_exports
  copy:
    src: exports
    dest: /etc/exports
    mode: "0777"

- name: 04_started_nfs
  systemd:
    name: nfs-server
    state: started
    enabled: yes
```

1. 编辑`roles`的 playbook

```bash
# site.yml
- name: nfs_server
  hosts: nfs_servers
  roles:
    - nfs_server
```

**创建**`**Role**`

1. 使用`ansible-galaxy`命令创建`role`骨架：

```bash
ansible-galaxy init role-name
```

1. 手动创建目录结构

`**Role**`**路径**

默认路径在`/etc/ansible/role`

自定义路径有两种方法指定：

1. 在配置文件中指定`roles`的搜索目录

```bash
[defaults]
# 可以指定多个路径，用冒号(:)分隔
roles_path = /path/to/your/roles:/another/path/to/roles
```

1. 在`playbook`中使用绝对路径或相对路径

```bash
- hosts: webservers
  roles:
    - /full/path/to/your/role
    - ../relative/path/to/role  # 相对路径也可以
```

**优化**

在当前我们学到的`roles`中，`tasks`目录中的`main.yaml`依旧包含了我们所有的任务。其实换汤不换药，依旧非常的难以管理。我们可以将每个任务写成一个单独的`yaml`文件，再在`main.yaml`里引入对应的`yaml`文件。

旧版写法：

```bash
vim tasks/main.yaml
- include: install.yaml
- include: group.yaml
- include: user.yaml
- include: copy.yaml
- include: systemd.yaml
```

新版写法：

```bash
# tasks/main.yaml
- ansible.builtin.include_tasks: install.yaml
- ansible.builtin.include_tasks: group.yaml
- ansible.builtin.include_tasks: user.yaml
- ansible.builtin.include_tasks: copy.yaml
- ansible.builtin.include_tasks: systemd.yaml
```

**include 模块**

上述例子中的引入使用到`include`模块。旧版的`include`模块是一个大类，可以直接导入任务文件、角色等等。而在新版中做了拆分：

| 模块            | 用途         | 示例                       |
| --------------- | ------------ | -------------------------- |
| `include_tasks` | 包含任务文件 | `include_tasks: setup.yml` |
| `import_tasks`  | 静态导入任务 | `import_tasks: common.yml` |
| `include_role`  | 动态包含角色 | `include_role: name=mysql` |
| `import_role`   | 静态导入角色 | `import_role: name=nginx`  |
| `include_vars`  | 包含变量文件 | `include_vars: vars.yml`   |

区别：

```bash
1. 加载时机不同
   - `import_*`: 在Playbook解析阶段静态加载（预编译）
   - `include_*`: 在运行时动态加载（按需执行）

2. 条件执行支持
   - `import_tasks/role`:
      不能与`when`条件共用
      不能用于`loop`循环
   - `include_tasks/role`:
      支持`when`条件判断
      支持`loop`循环迭代

3. 变量作用域
   - `import_*`: 使用"定义时"的变量值（静态作用域）
   - `include_*`: 使用"调用时"的变量值（动态作用域）

4. 执行次数
   - `import_role`: 只执行一次（即使被多次引用）
   - `include_role`: 每次调用都会执行

5. 标签(Tags)处理
   - `import_*`: 继承被导入文件的所有tags
   - `include_*`: 仅继承调用时指定的tags

6. 错误处理
   - `import_*`: 解析阶段报错（验证更严格）
   - `include_*`: 运行时才会报错（更灵活）

7. 性能比较
   - `import_*`: 解析开销大但执行快（适合稳定代码）
   - `include_*`: 解析快但执行稍慢（适合动态场景）
```

#### Template

`ansible`模板（`Templates`）是使用`Jinja2`模板引擎的强大功能，允许创建动态配置文件。

**基础概念**

1. 模板文件：以`.j2`为扩展名的文件，包含静态内容和动态变量
2. `Jinja2`：`Python`的模块引擎，提供变量替换、控制结构等功能
3. 模板模块：`template`模块用于处理模板文件

**示例：**

```bash
  tasks:
    - name: Copy template configuration
      ansible.builtin.template:
        src: templates/nginx.conf.j2
        dest: /etc/nginx/nginx.conf
        owner: root
        group: root
        mode: '0644'
```

**范例：**

使用`roles`的方式结合`Template`实现目标主机的`SSH`配置文件中的`Listen`修改为各自主机的`IP`地址。