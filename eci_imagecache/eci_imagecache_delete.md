# eci imagecache delete

## 用途
删除指定镜像缓存。

## 用法
```
eci imagecache delete [FLAGS] IMAGECACHE_IDS
```

## 示例
### 删除单个镜像缓存
```
eci imagecache delete imc-xxx
```

### 删除多个镜像缓存
```
eci imagecache delete $(eci imagecache list -n my-imc -q)
```
以上是两条命令的组合，首先执行list命令找出所有名为`my-imc`的镜像缓存，且只输出它们的ID，然后delete命令根据这些ID删除相应的镜像缓存。

## 更多选项
```
eci imagecache delete --help
```

