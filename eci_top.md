# eci top

## 用途
持续打印部分或所有实例的运行指标，并按指定字段排序。此命令与`eci stats`不同，`eci top`展示整个实例的运行指标，`eci stats`展示单个实例中每个容器的运行指标。

## 用法
```
eci top [FLAGS] [ECI_IDS]
```

## 示例
### 将指标转换为易读格式[-r]
```
eci top -r
```

### 按指定字段排序[-s]
所有可用值见命令输出中的标题行，当不指定该选项时，默认按`CPU_USED`字段排序所有实例。
```
eci top -s MEM_USED
```

### 设置刷新间隔[-d]
以秒为单位的整数，最小值为15。
```
eci top -r -d 20
```

### 只展示部分实例
```
eci top $(eci ps -t t1=v1 | sed 1d | awk '{print $1}')
```
其中`$(eci ps -t t1=v1 | sed 1d | awk '{print $1}')`用于筛选像展示的实例，并截取它们的ID，然后`eci top`根据这些ID展示相应实例的运行指标。

## 更多选项
```
eci top --help
```

