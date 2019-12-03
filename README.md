# ElephantOS
《操作系统真象还原》

## 小端字序&大端字序

> 小端字节序是数值的低字节放在内存的低地址处，数值的高字节放在内存的高地址。

> 大端字节序是数值的低字节放在内存的高地址处，数值的高字节放在内存的低地址。

**优点:**

> 小端：因为低位在低字节，强制转换数据型时不需要再调整字节了。 

> 大端：有符号数，其字节高位不仅表示数值本身，还起到了符号的作用。符号位固定为第一字 节，也就是高位占据低地址，符号直接可以取出来，容易判断正负。 

## 堆栈

> 堆是堆，栈是栈，大多数人之所以弄混，估计是因为大家都是那么叫的吧，不过我猜测是，因为在C语言里面栈是从高地址向低地址增减少，而堆则是从低地址向高地址增加，它们没有界限，所以到了一定的程度堆和栈一定会相遇。可能是基于这个考虑，大家才共同统一叫做堆栈吧。

## 实模式内存布局

 起始 | 结束 | 大小 | 用途 
 :-: | :-: | :-: | :-:  
 FFFF0 | FFFFF | 16B      | BIOS 入口地址，此地址也属于 BIOS 代码，同样属于顶部的 640KB 字节。只是为了 强调其入口地址才单独贴出来。此处 16 字节的内容是跳转指令 jmp f000：e05b
 F0000 | FFFEF | 64KB-16B | 系统 BIOS 范围是 F0000～FFFFF 共 640KB，为说明入口地址，将上面的 16 字节从此处去掉了，所以此处终止地址是 0XFFFEF 
 C8000 | EFFFF | 160KB    | 映射硬件适配器的 ROM 或内存映射式 I/O 
 C0000 | C7FFF | 32KB     | 显示适配器 BIOS 
 B8000 | BFFFF | 32KB     | 用于文本模式显示适配器 
 B0000 | B7FFF | 32KB     | 用于黑白显示适配器
 A0000 | AFFFF | 64KB     | 用于彩色显示适配器 
 9FC00 | 9FFFF | 1KB      | EBDA（Extended BIOS Data Area）扩展 BIOS 数据区 
 7E00  | 9FBFF | 622080B 约 608KB | 可用区域 
 7C00  | 7DFF  | 512B     | MBR 被 BIOS 加载到此处，共 512 字节 
 500   | 7BFF  | 30464B 约 30KB | 可用区域 
 400   | 4FF   | 256B     | BIOS Data Area（BIOS 数据区） 
 000   | 3FF   | 1KB      | Interrupt Vector Table（中断向量表） 
 
 ## BIOS是如何启动的
 
 > 计算机加电之后CPU的CS:IP被强制初始化为0xF000:0xFFF0，即0xFFFF0的位置，这个地址就是BIOS的起始地址
 
