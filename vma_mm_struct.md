# 虚拟存储管理的数据结构

叶子鹏 2013011404

## vma_struct和mm_struct的关系是什么？

在mm/vmm.h中定义：

```
// the virtual continuous memory area(vma), [vm_start, vm_end), 
// addr belong to a vma means  vma.vm_start<= addr <vma.vm_end 
struct vma_struct {
    struct mm_struct *vm_mm; // the set of vma using the same PDT 
    uintptr_t vm_start;      // start addr of vma      
    uintptr_t vm_end;        // end addr of vma, not include the vm_end itself
    uint32_t vm_flags;       // flags of vma
    list_entry_t list_link;  // linear list link which sorted by start addr of vma
};
```

```
// the control struct for a set of vma using the same PDT
struct mm_struct {
    list_entry_t mmap_list;        // linear list link which sorted by start addr of vma
    struct vma_struct *mmap_cache; // current accessed vma, used for speed purpose
    pde_t *pgdir;                  // the PDT of these vma
    int map_count;                 // the count of these vma
    void *sm_priv;                   // the private data for swap manager
};
```

这一块的描述需要结合下面的问题，单独说一个结构而不说其方法是无法解释清楚的。





## 描述进程的虚拟地址空间、页表项、物理页面和后备页面的关系

### 虚拟地址空间

程序所使用的空间，这个空间被虚拟成4G(对于32位)，这些虚拟页面会在二级页表中和物理页帧映射。

管理虚拟地址空间的结构是 mm/swap.h中的`swap_manager`，以及上述的两个结构。

按照面向对象的说法，`swap_manager`是一个接口，可以对应不同的方法来管理虚拟地址空间。
而`vma_struct`和`mm_struct`是对我们需要管理的页面的抽象，是属性。
`属性`加`方法`就是一个完整的类了，这个类就是ucore中管理虚拟地址的类。
(只不过实现是用C的实现)

### 页表项

页表是虚拟地址和对应的物理页面的一个映射。
页表项是存储某个特定的虚拟地址与其对应的物理页面的映射。

### 物理页面

物理页面是和页帧一一对应的，或者说是管理页帧时的一种抽象。ucore里使用Page这个结构来表示。

### 后备页面

即对换区，在硬盘上。当发生页缺失的时候，中断服务例程会访问disk去读取，这个过程称为换入换出。

对应的代码是mm/vmm.c中`do_pgfault`会调用`swap_in`，定义在mm/swap.c中。这个函数会从扇区换入页面。

