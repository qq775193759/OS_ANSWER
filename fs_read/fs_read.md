# 读文件的执行过程

叶子鹏 2013011404
沈哲言 2013011377

## 文件系统的启动

```
                                                 -->sem_init
                   -->vfs_init-->vfs_devlist_init-->list_init
kern_init-->fs_init-->dev_init-->init_device
                   -->sfs_init-->sfs_mount
```

## 读文件的执行过程

```
file_open-->fd_array_alloc
         -->vfs_open-->vfs_lookup
                    -->vop_open
                    -->vop_open_inc
         -->fd_array_open-->fopen_count_inc
```

```
file_read-->fd2file
         -->fd_array_acquire-->fopen_count_inc
         -->vop_read
         -->fd_array_release
```

```
file_close-->fd2file
```