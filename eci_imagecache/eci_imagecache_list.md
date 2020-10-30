# eci imagecache list

## 用途
查看当前账号下所有镜像缓存。

## 用法
```
eci imagecache list [FLAGS]
```

## 示例
### 按名字过滤镜像缓存[-n]
```
eci imagecache list -n my-imc
```
不同的镜像缓存可以拥有相同的名字，所以该命令将展示所有名字为centos的镜像缓存。

### 指定输出格式[-o]
```
eci imagecache list -o fixed
```
该选项所有可用值：
`wide`: 显示所有字段，当内容过长时，将自然地发生换行行为。
`ids`: 只显示ID列，且不包括标题行。
`fixed`: 显示所有字段，将屏幕宽度平均分配给每个字段，当字段内容过长时，将裁剪掉超出的部分。

### 只显示ID[-q]
效果与`-o ids`相同。
```
eci imagecache list -q
```

## 更多选项
```
eci imagecache lis --help
```

