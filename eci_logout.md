# eci logout

## 用途
移除指定镜像注册中心（Registry）的登录用户名和密码。

## 用法
```
eci logout [FLAGS] [REGISTRY_SERVER_ADDRESS]
```

## 示例
### 移除阿里容器镜像服务（ACR）认证
```
eci logout registry-vpc.cn-shanghai.aliyuncs.com
```

### 移除Docker官方镜像服务认证
```
eci logout
```

## 更多选项
```
eci logout --help
```

