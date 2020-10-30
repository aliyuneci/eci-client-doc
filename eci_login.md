# eci login

## 用途
保存指定镜像注册中心（Registry）的登录用户名和密码，以便让ECI有权限下载私有仓库镜像。

需要注意的是，ECI-Client不会校验你的凭证，而只是存储在本地文件中，只有在触发下载镜像的时候才知道你的凭证是否正确。

保存后的用户名和密码会作用于以下命令：
- `eci run`
- `eci update`
- `eci cg create`
- `eci cg update`
- `eci ic create`

## 用法
```
eci login [FLAGS] [REGISTRY_SERVER_ADDRESS]
```

## 示例
### 登录到阿里容器镜像服务
```
eci login registry-vpc.cn-shanghai.aliyuncs.com
```

### 登录到Docker官方镜像服务
```
eci login
```

## 更多选项
```
eci login --help
```

