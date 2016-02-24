#lab0 SPOC思考题

沈哲言 && 叶子鹏

###何处设置的中断使能？

通过asm(STI)语句

###系统何时处于中断屏蔽状态？

在asm(STI)之前和中断处理程序alltraps执行时。我们没有亲测中断不能嵌套，因为我们等不到时钟中断，但是我们通过文档中的RTI的if has pending interrupt, process the interrupt可知。

###如果系统处于中断屏蔽状态，如何让其中断使能？

通过asm(STI)语句中断使能，通过CLI屏蔽中断。

###系统产生中断后，CPU会做哪些事情？（在没有软件帮助的情况下）

先切换到内核态

###CPU执行RTI指令的具体完成工作是哪些？


