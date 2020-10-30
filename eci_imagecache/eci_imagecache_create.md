# eci imagecache create

## 用途
创建镜像缓存。

## 用法
```
eci imagecache create [FLAGS]
```

## 示例
### 创建镜像缓存
创建镜像缓存需要先编写一个模板文件：`ic-nginx.yaml`。
```
ImageCacheName: ic-nginx
Image: ["nginx:1.19.1", "centos:7.7.1908"]
ImageCacheSize: 20
ImageRegistryCredential:
- Server: docker.io
  UserName: jack
  Password: pass123
```

然后通过`-f`选项指定它。
```
eci imagecache create -f ic-nginx.yaml
```

也可以将文件写入到标准输入。
```
eci imagecache create < ic-nginx.yaml
```

## 更多选项
```
eci imagecache create --help
```

