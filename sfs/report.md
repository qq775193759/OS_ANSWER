# SYS����

Ҷ���� 2013011404 ������ 2013011371

## ����1�� 
����[sfs�ļ�ϵͳ��״̬�仯��Ϣ](./sfs_states.txt)������������ļ���ز�������.

��ϸ������ļ���д��2������֮��Ϳ��Կ���ÿһ������Ҫ�������顣

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

���һ���ʹ�Ҳ�̫һ����Ҳ���ǰ汾���⡣

## ����2��
��[sfs-homework.py �ο�����Ļ�����](https://github.com/chyyuu/ucore_lab/blob/master/related_info/lab8/sfs-homework.py)��
ʵ�� `writeFile, createFile, createLink, deleteFile`��ʹ�����ʵ���ܹ��ﵽ������1����ȷ���һ��

��ϸ�����롣

ɾ����ʵ�ֵĹ��̽���˱��Ҹ���ش��ͬѧ�����ǲ���Ҫ�õ�ɾ��������
