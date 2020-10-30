# eci images

## 用途
查看当前账户中（[CR产品](https://cr.console.aliyun.com/)）所有镜像和版本。

## 用法
```
eci images [FLAGS]
```

## 示例
### 指定输出格式[-o]
```
eci images -o fixed
```
该选项所有可用值：
`wide`: 显示所有字段，当内容过长时，将自然地发生换行行为。
`ids`: 只显示ID列，且不包括标题行。
`fixed`: 显示所有字段，将屏幕宽度平均分配给每个字段，当字段内容过长时，将裁剪掉超出的部分。

### 只显示ID[-q]
效果与`-o ids`相同。
```
eci images -q
```

## 更多选项
```
eci images --help
```

