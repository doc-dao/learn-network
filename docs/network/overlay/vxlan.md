# VXLAN

VXLAN是一种承载协议，定义了MAC-over-UDP的封装方案，由内（inner）到外（outer）分别增加了8字节VXLAN头部，8字节UDP头部，20字节IP头部和14字节以太网头部，合计增加了50字节封装。

![](/img/vxlan.png)

## Intro
1. [启迪云谈 | VXLAN篇](https://zhuanlan.zhihu.com/p/43731577): 基本介绍加header格式


