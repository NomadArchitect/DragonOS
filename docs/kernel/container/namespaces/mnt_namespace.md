# 挂载命名空间

## 底层架构

pcb -> nsproxy -> mnt_namespace

每一个挂载文件系统都有自立独立的挂载点，表现在数据结构上是一个挂载的红黑树，每一个命名空间中挂载是独立的，所以文件系统的挂载和卸载不会影响别的

## 系统调用接口
 

- clone
    - CLONE_NEWNS用于创建一个新的 MNT 命名空间。提供独立的文件系统挂载点
- unshare 
    - 使用 CLONE_NEWPID 标志调用 unshare() 后，后续创建的所有子进程都将在新的命名空间中运行。
- setns
    - 将进程加入到指定的命名空间
- chroot 
    - 将当前进程的根目录更改为指定的路径，提供文件系统隔离。