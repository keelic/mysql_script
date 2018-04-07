# 二进制包安装 

**作者：** keelic  
**日期：** 2018-04-07    

```shell
# 安装环境Ubuntu-16.04.1

# 1.下载安装包，解压
cd ~/downloads/
wget https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.21-linux-glibc2.12-x86_64.tar.gz
sudo mkdir /usr/local/opt
sudo tar -xvf mysql-5.7.21-linux-glibc2.12-x86_64.tar.gz -C /usr/local/opt/

# 2.创建用户及必要文件夹
sudo groupadd mysql
sudo useradd -r -g mysql -s /bin/false mysql
sudo mkdir -p /data/mysql/db3306/{data,log,tmp}

# 3.创建软链接及授权
# 在/usr/local目录下创建软链接，给使用者提供一个统一的路径
sudo ln -s /usr/local/opt/mysql-5.7.21-linux-glibc2.12-x86_64/ /usr/local/mysql
sudo chown -R mysql:mysql /usr/local/mysql/
sudo chown -R mysql:mysql /data/mysql

# 4.使用配置文件初始化数据库
# 编辑配置文件
vim /data/mysql/db3306/db3306.cnf
# 数据库初始化（会生成一个临时密码）
sudo /usr/local/mysql/bin/mysqld --defaults-file=/data/mysql/db3306/db3306.cnf --initialize --user=mysql

# 5.启动和登录数据库
sudo /usr/local/mysql/bin/mysqld_safe --defaults-file=/data/mysql/db3306/db3306.cnf &
/usr/local/mysql/bin/mysql -uroot -p

# 6.初次修改登录密码
mysql> alter user 'root'@'localhost' identified by '123abc';
mysql> flush privileges;


# 配置环境变量（可以修改/etc/profile文件永久生效）
export PATH="/usr/local/mysql/bin:$PATH"

```
