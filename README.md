# 个人自助云面板，支持Azure Aws Do、Linode等云厂商

 安装docker
```
curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh 
```

 如果docker没启动，可以运行这个
```
service docker start
```
 docker创建网络
```
docker network create cdntip_network 
```

 启动mysql容器 (更换mysqlroot密码后，机器内部也需要修改database.conf文件的密码)
```mkdir /data 
docker run -d -it --network cdntip_network -v /data/mysql:/var/lib/mysql --name panel_mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=panel mysql:5.7 --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
```

 启动 cloudpanel (8111端口可改为任意，此处为实际对外端口)
```
docker run -d -it --network cdntip_network -p 8111:80 --name panel tiktokmjj/openpanel 
```

 进入容器
```
docker exec -it panel /bin/bash
```

 创建管理员
```
python manage.py createsuperuser --username 管理员账户 --email 管理员邮箱
```
示例：python manage.py createsuperuser --username admin --email 123456@qq.com

 添加aws镜像
```
python manage.py aws_update_images
```

# 其他功能
停止当前容器 
```
docker stop panel
```
删除当前容器
```
docker rm panel
```
# 演示效果
![image](https://user-images.githubusercontent.com/55003092/202330238-0ba46d1b-4e22-407f-b02f-bf4802a3f85e.png)

