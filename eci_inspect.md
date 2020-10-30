# eci inspect

## 用途
查看指定实例的详细信息。

## 用法
```
eci inspect [FLAGS] [ECI_ID]
```

## 示例
### 指定输出格式[-o]
```
eci inspect --output json eci-xxx
```
该选项目前有两个值：json和yaml

### 查看指定名字的实例[-n]
```
eci inspect -n centos
```
不同ECI实例名字可以相同，该命令将匹配所有名字为`centos`的实例。

### 查看通过指定模板创建的实例[-f]
当通过yaml模板创建了一个实例后，可以通过指定该yaml模板，来查看实例的详细信息。该命令会读取模板中的实例名字，然后用该名字来查找匹配的实例。
```
eci inspect -f my-eci.yaml
```

## 更多选项
```
eci inspect --help
```

