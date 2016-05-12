# SYS报告

叶子鹏 2013011404 沈哲言 2013011371

## 问题1： 
根据[sfs文件系统的状态变化信息](./sfs_states.txt)，给出具体的文件相关操作内容.

详细见结果文件，写完2个函数之后就可以看到每一步操作要做的事情。

```
mkdir("/g");

creat("/q");

creat("/u");

link("/u", "/x"); 

mkdir("/t");

creat("/g/c");

unlink("/x");

mkdir("/g/w");

fd=open("/g/c", O_WRONLY|O_APPEND); write(fd, buf, BLOCKSIZE); close(fd);

fd=open("/g/c", O_WRONLY|O_APPEND); write(fd, buf, BLOCKSIZE); close(fd);
```

最后一步和大家不太一样，也许是版本问题。

## 问题2：
在[sfs-homework.py 参考代码的基础上](https://github.com/chyyuu/ucore_lab/blob/master/related_info/lab8/sfs-homework.py)，
实现 `writeFile, createFile, createLink, deleteFile`，使得你的实现能够达到与问题1的正确结果一致

详细见代码。

删除的实现的过程借鉴了比我更早回答的同学。但是并需要用到删除操作。
