### 使用令行管理 headscale 服务器

弄清楚命令行管理的方式，网页界面的自然就懂了。

#### 用户管理

使用 headscale 创建用户信息

```shell
headscale users create myfirstuser

# 容器中使用
# docker exec headscale headscale users create myfirstuser
```

新建 user 用户的 preauthkey 授权密钥，该密钥之后用来添加用户节点时作为参数使用。

- preauthkey 可重复使用使用 `reusable` 和 过期时间 `expiration` 的参数。 
- 一个 key 最多只能添加一个节点，如果要添加新节点，则创建新的 key。

```shell
headscale preauthkeys create --user myfirstuser --reusable --expiration 9999d

# 容器中使用
# docker exec headscale headscale preauthkeys create --user su-pve --reusable --expiration 9999d
```

![[#^d82d4b]]


查看连接情况
```shell
headscale nodes list

# 容器中使用
# docker exec headscale headscale nodes list

```

^16113f


#### apikey 的管理 

```shell
headscale apikeys create --expiration 9999d
```


#### 节点管理

对节点的增删改查。


```shell
# 显示节点、用户、路由的列表
headscale nodes ls
headscale users ls
headscale routes ls

# 查看 key
headscale preauthkeys --user default list

# 删除节点
headscale nodes delete -i <id>


# 启动服务
systemctl start headscale
# 开机自启
systemctl enable headscale
# 查看状态
systemctl status headscle

```



