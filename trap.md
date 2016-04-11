# 用户态或内核态下的中断处理有什么区别？在trapframe中有什么体现？

叶子鹏 2013011404

主要体现在硬件的处理方式不同。当然，软件针对硬件的不同行为，也会有所区别。

+ 在进入中断时保存的现场不同。
+ 在退出时恢复现场不同。

从用户态进入中断时，硬件会压入一些信息到栈帧中，需要先压入ss和esp，再压入4个信息（error code，cs，eip，eflags），而从内核态进入中断时，只需要压入那4个信息。这在trapframe中有所体现。

从中断返回时，硬件会从栈帧中pop一些信息。对应进入中断，中断返回pop的数量是相同的。如果返回到用户态，则会pop出6个信息，如果返回到内核态，只pop出4个信息。

```
struct trapframe {
    struct pushregs tf_regs;
    uint16_t tf_gs;
    uint16_t tf_padding0;
    uint16_t tf_fs;
    uint16_t tf_padding1;
    uint16_t tf_es;
    uint16_t tf_padding2;
    uint16_t tf_ds;
    uint16_t tf_padding3;
    uint32_t tf_trapno;
    /* below here defined by x86 hardware */
    uint32_t tf_err;
    uintptr_t tf_eip;
    uint16_t tf_cs;
    uint16_t tf_padding4;
    uint32_t tf_eflags;
    /* below here only when crossing rings, such as from user to kernel */
    uintptr_t tf_esp;
    uint16_t tf_ss;
    uint16_t tf_padding5;
} __attribute__((packed));
```

可以看出，最后2个属性esp和ss仅仅从user to kernel