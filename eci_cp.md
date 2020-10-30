# eci cp

## 用途
用于在ECI实例和本地文件系统之间复制文件或目录。需要注意的是，此功能依赖于远程容器中的`sh`和`tar`程序，如果实例中不含有这些程序，则命令会执行失败。

## 用法
```
eci cp [FLAGS] [ECI_ID:]PATH [ECI_ID:]PATH
```

## 示例
### 复制本地文件到实例中
将本地文件/local/src拷贝到ECI实例eci-xxx的/path/dest目录下。
```
eci cp /local/src eci-xxx:/path/dest
```
其中src是本地的文件或目录，`/path/dest`代表实例中的目标位置，`/path`必须是在实例中已存在的目录，此时ECI会将src复制到`/path`目录下，紧接着把src更名为dest。当目标路径为`/path/dest/`形式时，则`/path/dest`必须是一个已存在的目录，此时ECI会将src复制到`/path/dest`目录下，最终目标路径为`/path/dest/src`。

### 复制实例中的文件到本地
将ECI实例eci-xxx中的`/src`复制到本地的`/path/dest`，规则与上面相同。
```
eci cp eci-xxx:/src /local/dest
```

## 更多选项
```
eci cp --help
```
