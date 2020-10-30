# eci update

## 用途
更新指定实例，该命令有两种方式更新实例，一种是通过命令行，该方式适用于只含有一个容器的实例，且只能更新少数字段；另一种是通过-f选项指定一个yaml模板文件（该文件通常是创建实例时所用的文件，见命令：`eci run`），该方式支持更新更多的ECI参数，所有可用参数见[ECI SDK](https://api.aliyun.com/#/?product=Eci&version=2018-08-08&api=UpdateContainerGroup&params={}&tab=DOC&lang=JAVA)。

## 用法
```
eci update [FLAGS] ECI_ID
```

## 示例
### 更新容器镜像[--image]
```
eci update eci-xxx --image nginx:2.0
```
该命令只更新实例中第一个容器的image，当实例中含有多个容器时，命令将中断执行。

## 更多选项
```
eci update --help
```

