# actor与actor通信

1.函数

2.蓝图接口

3.事件分发器

4.直接引入actor引用


# UI与UI之间使用通信的方法
1. 函数

2.蓝图接口

3.事件分发器

其中事件分发器使用最便捷，因为不需要两个UI有交互，可以隔空互调方法
1.首先写下一个事件分发器，写清在什么情况下会调用这个事件分发器，重点是要生成事件
![[1.png]]

2.然后把这个UI加入到需要用到这个功能的UI中，
![[Pasted image 20241121092739.png]]
