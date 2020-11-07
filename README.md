使用docker部署nginx，php，mysql环境

1. 创建用户
```bash
useradd -M -s /sbin/nologin -u 1000 -g 1000 ptadmin
```

2.修改.evn文件
将`RUN_UID`和`RUN_GID`改成ptadmin的uid和gid
```bash
RUN_UID=1000
RUN_GID=1000
```
