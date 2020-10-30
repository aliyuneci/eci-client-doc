# eci config set-context

## 用途
增加或修改一个配置上下文，一个配置上下文代表一组用户配置，比如阿里云访问密钥、默认地区ID、默认安全组ID、默认交换机ID等。配置文件默认保存在`~/.eci/config`。

## 用法
```
eci config set-context [FLAGS]
```

## 示例
### 新增一个上下文
```
eci config set-context \
--access-key-id XXXxxx \
--access-secret XXXxxx \
--security-group-id sg-xxx \
--v-switch-id vsw-xxx \
--region-id cn-beijing \
-x bj
```
说明：
- `-x`：指定上下文的名字，如果未指定该选项，上下文将被命名为`default`。
- `--access-key-id`, `--access-secret`：[阿里云密钥对](https://usercenter.console.aliyun.com/)，用于在连接阿里云时认证用户身份。
- `--region-id`：指定默认地区，如杭州（cn-hangzhou）、北京（cn-beijing）等，使用命令`eci region list`查看所有可用地区，实例的创建查询等都需要指定地区。
- `--v-switch-id`：指定默认[虚拟交换机](https://help.aliyun.com/document_detail/100380.html)，用于创建ECI实例。
- `--security-group-id`：指定默认[安全组](https://help.aliyun.com/document_detail/25387.html)，用于创建ECI实例。

### 自动初始化网络资源[--init]
如果你首次使用ECI产品，还没有创建过专有网络和安全组等必要的网络资源，则可以使用以下命令完成配置，它将在默认地区自动创建所需的网络资源，这些资源均以`eci-cli-init-xxxxx`形式命名，你可以在阿里云控制台找到它们。
```
eci config set-context \
--access-key-id XXXxxx \
--access-secret XXXxxx \
--init
```

### 自动清理网络资源[--clean]
使用该选项删除所有以`eci-cli-init-`为前缀的网络资源，如果有任何ECI实例还在使用这些资源，该命令将不会执行任何删除操作。
```
eci config set-context \
--access-key-id XXXxxx \
--access-secret XXXxxx \
--clean
```

### 修改指定上下文
```
eci config set-context \
--security-group-id sg-xxx \
-x bj
```
该命令将上下文bj的安全组ID修改为`sg-xxx`，选项`-x`指定了上下文的名字，如果未指定该选项，将修改名字为`default`的上下文。

### 临时指定上下文[-x]
假设我们现在已经增加了两个上下文，一个为北京地区，命令为bj；一个为上海地区，命名为sh。则在执行任意命令时都可以临时指定其中一个上下文，以下命令将使用sh上下文查询所有实例。
```
eci ps -x sh
```

## 更多选项
```
eci config set-context --help
```

