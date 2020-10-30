# eci rm

## 用途
删除指定实例。

## 用法
```
eci rm [FLAGS] ECI_IDS
```

## 示例
### 删除单个实例
```
eci rm eci-xxx
```

### 删除多个实例
```
eci rm $(eci ps -t t1=v1 -q)
```
以上是两条命令的组合，首先执行ps命令找到所有带有标签`t1=v1`的实例，且只输出它们的ID，然后rm命令根据这些ID删除相应的实例。

## 更多选项
```
eci rm --help
```

