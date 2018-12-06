# 阿里云服务器CentOS的配置总结


## SSH安全加固

1. 设置密码失效时间
```
在 /etc/login.defs 中将 PASS_MAX_DAYS 参数设置为 60-180之间，如 PASS_MAX_DAYS 90。
需同时执行命令设置root密码失效时间： $ chage --maxdays 90 root。
```
1. 设置密码修改最小间隔时间
```
在 /etc/login.defs 中将 PASS_MIN_DAYS 参数设置为5-14之间,建议为7： PASS_MIN_DAYS 7 
需同时执行命令为root用户设置： $ chage --mindays 7 root
``` 
1. 禁止SSH空密码用户登录
```
在/etc/ssh/sshd_config中取消PermitEmptyPasswords no注释符号#
```
1. 确保SSH MaxAuthTries设置为3到6之间
```
在/etc/ssh/sshd_config中取消MaxAuthTries注释符号#，设置最大密码尝试失败次数3-6，建议为5：MaxAuthTries 5
```
1. SSHD强制使用V2安全协议
```
编辑 /etc/ssh/sshd_config 文件以按如下方式设置参数： Protocol 2
```
1. 设置SSH空闲超时退出时间

```
编辑/etc/ssh/sshd_config，将ClientAliveInterval 设置为300到900，即5-15分钟，将ClientAliveCountMax设置为0。 
ClientAliveInterval 300 ClientAliveCountMax 0
```
1. 确保SSH LogLevel设置为INFO
```
编辑 /etc/ssh/sshd_config 文件以按如下方式设置参数(取消注释): LogLevel INFO
```
1. 设置用户权限配置文件的权限
```
执行以下5条命令 
$ chown root:root /etc/passwd /etc/shadow /etc/group /etc/gshadow 
$ chmod 0644 /etc/group 
$ chmod 0644 /etc/passwd 
$ chmod 0400 /etc/shadow 
$ chmod 0400 /etc/gshadow
```
