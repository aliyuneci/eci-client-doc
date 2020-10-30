# eci ps

## 用途
查看当前账号下且当前Region下已创建的实例，同时提供多个选项来筛选要展示的实例。

## 用法
```
eci ps [FLAGS] [ECI_IDS]
```

## 示例
### 查看所有实例
```
eci ps
```

### 按名字过滤实例[-n]
```
eci ps -n centos
```
不同ECI实例名字可以相同，该命令将展示所有名字为`centos`的实例。

### 按状态过滤实例[-s]
```
eci ps -s Pending
```
该选项所有可用值：Scheduling|Pending|Updating|Restarting|ScheduleFailed|Failed|Expired|Running|Terminating|Succeeded

### 按标签过滤实例[-t]
```
eci ps -t name=jack -t age=18
```

### 按zone-id过滤实例[-z]
```
eci ps -z ch-shanghai-g
```

### 指定输出格式[-o]
```
eci ps --output simple
```
该选项所有可用值：
`simple`: 显示少量字段。
`wide`: 显示所有字段，当内容过长时，将自然地发生换行行为。
`ids`: 只显示ID列，且不包括标题行。
`fixed`: 显示所有字段，将屏幕宽度平均分配给每个字段，当字段内容过长时，将裁剪掉超出的部分。

### 只显示ID[-q]
效果与`-o ids`相同。
```
eci ps -q
```

## 更多选项
```
eci ps --help
```

