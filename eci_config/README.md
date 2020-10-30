# [eci_config](#eci_config)

## 用途
该命令下包含多个子命令，用于增加、切换、删除、查看用户配置上下文（context），一个配置上下文代表一组用户配置，包含了阿里云访问密钥、默认区域ID、默认安全组ID、默认交换机ID等信息。配置文件默认保存在`~/.eci/config`。

## 用法
```
eci config [COMMAND]
```

## 命令列表
- [`eci config del-context`　-　删除一个配置上下文](eci_config_del-context.md)
- [`eci config list`　-　查看配置文件](eci_config_list.md)
- [`eci config set-context`　-　添加或修改指定配置上下文](eci_config_set-context.md)
- [`eci config use-context`　-　切换配置上下文](eci_config_use-context.md)
