# eci config use-context

## 用途
切换配置上下文。

## 用法
```
eci config use-context [FLAGS] CONTEXT_NAME
```

## 示例
### 切换上下文
```
eci config use-context sh
```
现在执行任何命令将默认使用名为sh的上下文。

### 临时指定上下文[-x]
假设我们现在已经增加了两个上下文，一个为北京地区，命令为bj；一个为上海地区，命名为sh。则在执行任意命令时都可以临时指定其中一个上下文，以下命令将使用sh上下文查询所有实例。
```
eci ps -x sh
```

## 更多选项
```
eci config use-context --help
```

