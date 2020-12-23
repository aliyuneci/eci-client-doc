# eci run

## 用途
创建并启动一个实例，该命令有两种方式创建实例，一种是通过命令行只给予必要的参数，创建一个只包含一个容器的实例；另一种是编写一个yaml模板文件（模板格式见本文尾部），该文件中可以自定义所有ECI参数，然后通过`-f`选项指定yaml文件，或者将文件写入到标准输入。

## 用法
```
eci run [OPTIONS] IMAGE [COMMANDS]
```

## 示例
### 为实例指定名字[-n]
使用centos7镜像创建一个实例，命名为myeci，`-n`选项不是必须的，ECI会默认为实例分配一个名字。
```
eci run -n myeci centos:7 sleep 3600
```

### 挂载数据卷[-v]
选项`-v`用于为实例挂载数据卷，该数据可以是已经存在的，也可以是不存在的。挂载时可以提供挂载选项，如磁盘大小（DiskSize）、文件系统格式（FileSystemType）等，但所有选项都是可选的，只有目标挂载路径（DEST_PATH）是必须的。选项`-v`的语法如下（选项顺序不分先后）：
```
[VolumeType][,DiskId][,DiskSize][,FileSystemType][,ReadOnly]:DEST_PATH
```
挂载选项说明：
- `VolumeType`：卷类型，可用值：`DiskVolume`(默认), `EmptyDirVolume`
- `DiskId`：云盘ID，用于挂载已存在的云盘到实例中，不会随实例的释放而释放
- `DiskSize`：云盘容量，用于自动创建磁盘，不可与`DiskId`同时使用，以GB为单位的整数，最小值20(默认)
- `FileSystemType`：文件系统类型，可用值：`xfs`(默认), `ext4`
- `ReadOnly`：是否以只读方式挂载，可用值：`ReadOnly`, `ro`

示例1，自动创建两块[阿里云盘](https://ecs.console.aliyun.com/)并挂载到实例中的`/data`和`/config`，当通过ECI命令行删除实例时，云盘自动删除。
```
eci run -v /data -v /config nginx
```

示例2，自动创建一块[阿里云盘](https://ecs.console.aliyun.com/)，指定云盘大小为100GB，文件系统格式为ext4，然后挂载到实例中的`/data`，当通过ECI命令行删除实例时，云盘自动删除。
```
eci run -v 100,ext4:/data nginx
```

示例3，挂载一块已存在的云盘，云盘ID为`d-xxx`，文件系统格式为xfs，挂载到实例中的`/data`，当通过ECI命令行删除实例时，云盘保留。
```
eci run -v d-xxx,xfs:/data nginx
```

### 公网IP和带宽[-w]
创建一个带有[弹性公网IP](https://ip.console.aliyun.com/)的实例，该公网IP带宽限制为5MB，当`-w`的值为0时，将不创建弹性公网IP。当通过命令行删除实例时，弹性公网IP实例也将被删除。
```
eci run -w 5 nginx
```

### 限制内存和CPU[-m, -c]
限制实例的可使用的最大内存和最大CPU核数，内存参数以GiB为单位，CPU参数以核为单位。
```
eci run -m 1.50 -c 0.25 nginx
```

### 指定环境变量[-e]
```
eci run -e k1=v1 -e k2=v2 nginx
```

### 通过yaml模板创建实例[-f]
通过yaml模板创建实例，先编写一个yaml模板文件`eci.yaml`：
```
ContainerGroupName: eci-centos8
Container:
- Name: centos8
  Image: centos:8.1.1911
  Command: ["bash", "-c", "while true; do date; sleep 10; done"]
  ImagePullPolicy: IfNotPresent
  VolumeMount:
  - Name: nas
    MountPath: /mnt/nas
    ReadOnly: false
Volume:
- Name: nas
  Type: NFSVolume
  NFSVolume:
    Server: xxxxx.xxxxx.nas.aliyuncs.com
    Path: /
    ReadOnly: false
ImageRegistryCredentials:
- Server: docker.io
  UserName: jack
  Password: jack123
```
然后使用该文件来创建实例：
```
eci run -f eci.yaml
```
注意，当使用yaml模板来创建实例时，除了`-f`和`-w`选项以外，其他选项都将被忽略，因为这些选项都是针对实例中某个容器的，如果模板中定义了多个容器，ECI将不知道这些选项应该作用于哪个容器。

## 更多选项
```
eci run --help
```

## 模板所有可用字段
每一个字段的具体含义见[SDK文档](https://api.aliyun.com/#/?product=Eci&version=2018-08-08&api=CreateContainerGroup&params={}&tab=DOC&lang=JAVA)。
```
ActiveDeadlineSeconds: ""
Arn: null
AutoMatchImageCache: ""
ClientToken: ""
ConnectTimeout: 0
Container:
- Arg: null
  Command:
  - sh
  - -c
  - while true; do date; sleep 10; done
  Cpu: "0.25"
  EnvironmentVar:
  - FieldRefFieldPath: ""
    Key: k1
    Value: v1
  - FieldRefFieldPath: ""
    Key: k2
    Value: "true"
  Gpu: "0.25"
  Image: busybox
  ImagePullPolicy: IfNotPresent
  LifecyclePostStartHandlerExec: null
  LifecyclePostStartHandlerHttpGetHost: ""
  LifecyclePostStartHandlerHttpGetHttpHeader: null
  LifecyclePostStartHandlerHttpGetPath: ""
  LifecyclePostStartHandlerHttpGetPort: ""
  LifecyclePostStartHandlerHttpGetScheme: ""
  LifecyclePostStartHandlerTcpSocketHost: ""
  LifecyclePostStartHandlerTcpSocketPort: ""
  LifecyclePreStopHandlerExec: null
  LifecyclePreStopHandlerHttpGetHost: ""
  LifecyclePreStopHandlerHttpGetHttpHeader: null
  LifecyclePreStopHandlerHttpGetPath: ""
  LifecyclePreStopHandlerHttpGetPort: ""
  LifecyclePreStopHandlerHttpGetScheme: ""
  LifecyclePreStopHandlerTcpSocketHost: ""
  LifecyclePreStopHandlerTcpSocketPort: ""
  LivenessProbe:
    Exec:
      Command: null
    FailureThreshold: ""
    HttpGet:
      Path: ""
      Port: ""
      Scheme: ""
    InitialDelaySeconds: ""
    PeriodSeconds: ""
    SuccessThreshold: ""
    TcpSocket:
      Port: ""
    TimeoutSeconds: ""
  Memory: ""
  Name: busybox
  Port: null
  ReadinessProbe:
    Exec:
      Command: null
    FailureThreshold: ""
    HttpGet:
      Path: ""
      Port: ""
      Scheme: ""
    InitialDelaySeconds: ""
    PeriodSeconds: ""
    SuccessThreshold: ""
    TcpSocket:
      Port: ""
    TimeoutSeconds: ""
  SecurityContext:
    Sysctl: null
  Stdin: ""
  StdinOnce: ""
  Tty: ""
  VolumeMount:
  - Name: nfs
    MountPath: /mnt/nfs
    ReadOnly: false
  WorkingDir: ""
Volume:
- Name: nfs
  Type: NFSVolume
  NFSVolume: 
    Server: xxxxx.xxxxx.nas.aliyuncs.com
    Path: /
    ReadOnly: false
ContainerGroupName: eci-busybox
Content: null
Cpu: "0.25"
DnsConfig:
  NameServer: null
  Option: null
  Search: null
DnsPolicy: ""
Domain: ""
EipInstanceId: ""
FormParams: {}
HostAliase: null
ImageRegistryCredential:
- Password:  pass123
  Server: docker.io
  UserName: eci-user
ImageSnapshotId: ""
InitContainer: null
InstanceType: ""
Ipv6AddressCount: ""
Memory: ""
Method: POST
NtpServer: null
OwnerAccount: ""
OwnerId: ""
Port: ""
QueryParams: {}
RamRoleName: ""
ReadTimeout: 0
RegionId: cn-shanghai
ResourceGroupId: ""
ResourceOwnerAccount: ""
ResourceOwnerId: ""
RestartPolicy: ""
Scheme: ""
SecurityContext:
  Sysctl: null
SecurityGroupId: sg-xxx
SlsEnable: ""
SpotPriceLimit: ""
SpotStrategy: ""
Tag:
- Key: t1
  Value: v1
- Key: t2
  Value: "true"
TerminationGracePeriodSeconds: ""
VSwitchId: vsw-xxx
VSwitchStrategy: ""
VkClientVersion: ""
ZoneId: ""
```

