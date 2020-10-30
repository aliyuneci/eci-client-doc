# eci imagecache describe

## 用途
查看指定镜像缓存的详细信息。

## 用法
```
eci imagecache describe [FLAGS]
```

## 示例
### 通过ID获取镜像缓存
```
eci imagecache describe imc-xxx
```

### 通过名字获取镜像缓存[-n]
```
eci imagecache describe -n my-ic-nginx
```

### 通过模板文件获取镜像缓存[-f]
```
eci imagecache describe -f ic-nginx.yaml
```

## 更多选项
```
eci imagecache describe --help
```

