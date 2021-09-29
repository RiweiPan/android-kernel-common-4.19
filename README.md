本文参考笨叔叔的实验环境配置~

编译内核
```shell
make debian_defconfig
make -j4
```

安装vm需要的文件
```shell
sh run_debian_x86_64.sh build_rootfs
```

启动vm
```shell
sh run_debian_x86_64.sh run
```
进入到vm，需要输入登录账号密码
```
username: root
password: 123
```

启动F2FS功能
```shell
make menuconfig
```
选择对应的F2FS功能启动, 然后重新编译内核
```shell
make -j4
```

重新进入到vm后，通过如下命令将f2fs挂载到data目录
```shell
mkdir data
mount -t f2fs -o mode="lfs" /dev/vdb data
```
**注意:** 在源码目录下会生产一个`flash0.img`，这个是f2fs磁盘的镜像，初始化时在`run_debian_x86_64.sh`里面设定了大小和格式，需要变化的可以手动通过`dd`命令和`mkfs.f2fs`命令创建F2FS镜像。当`flash0.img`因代码错误出现问题时，也可以通过`mkfs.f2fs`重新格式化为f2fs，重新挂载就行

