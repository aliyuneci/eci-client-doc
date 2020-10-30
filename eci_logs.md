# eci logs

## 用途
查看指定实例的日志输出。

## 用法
```
eci logs [FLAGS] ECI_ID
```

## 示例
### 查看最近10行日志[-t]
```
eci logs -t 10 eci-xxx
```

### 指定容器[-c]
当实例中包含多个容器时，可以通过该选项查看某一个容器的日志输出。
```
eci logs eci-xxx -c cnetos
```

## 更多选项
```
eci logs --help
```

