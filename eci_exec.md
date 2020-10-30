# eci exec

## 用途
用于在实例中执行命令行。

## 用法
```
eci exec [FLAGS] ECI_ID COMMAND [ARGS]
```

## 示例
### 为命令分配一个TTY设备并监听输入流[-t, -i]
```
eci exec -ti eci-xxx bash
```
`-t`选项将告诉bash以terminal方式启动，bash将会在执行命令时打印交互信息、为输出的数据着色等。
`-i`选项不是必须的，因为即使不加该选项，ECI也会监听输入流，以下的命令会被正确执行。
```
eci exec eci-xxx cat < file.txt
```

## 更多选项
```
eci ps --help
```

