1. 网卡设置

```shell
gkjuanmao@gkjuanmao:/etc/docker$ cat /etc/netplan/00-installer-config.yaml 
# This is the network config written by 'subiquity'
network:
  ethernets:
    ens33:
      addresses:
        - 192.168.3.34/24
      gateway4: 192.168.3.1
      nameservers:
          search: [mydomain, otherdomain]
          addresses: [8.8.8.8, 114.114.114.114]
      dhcp4: false
  version: 2
```



2. docker镜像源

```shell
{
  "registry-mirrors": ["https://y0qd3iq.mirror.aliyuncs.com"]
}
```

3. Mysql 8 设置远程连接

```shell
sudo docker run --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:8
sudo docker exec -it mysql bash
 mysql -u root -p
 ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';
 CREATE USER 'gkjuanmao'@'%' IDENTIFIED WITH mysql_native_password BY '123456';
 GRANT ALL PRIVILEGES ON *.* TO 'gkjuanmao'@'%';
 flush privileges;
```



