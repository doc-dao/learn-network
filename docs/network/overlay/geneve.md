# GENEVE

GENEVE与VXLAN类似，仍然是Ethernet over UDP，也就是用UDP封装Ethernet。VXLAN header是固定长度的（8个字节，其中包含24bit VNI），与VXLAN不同的是，GENEVE header中增加了TLV（Type-Length-Value），由8个字节的固定长度和0~252个字节变长的TLV组成。GENEVE header中的TLV代表了可扩展的元数据。我们来看一下GENEVE header：

![](https://pic4.zhimg.com/v2-cbaeba91beac2c214011036b72447067_b.jpg)

* Version（2bit）：没什么好说的，目前是0
* Opt Len（6bit）：以4字节为单位，表明Variable Length Options的长度。因为只有6bit，所以Variable Length Options最多是252（63*4）字节。
* O（1bit）：表明这是一个OAM包，包含了控制信息，而非数据。Endpoint可以根据这个bit来优先处理这个包。
* C（1bit）：表明在Variable Length Options里面，存在一个或者多个Critical的option。当C被置位时，Variable Length Options必须被解析，如果当前Endpoint不支持GENEVE解析，那么应该丢弃数据包。如果C没有被置位，那么Endpoint可以根据Opt Len直接丢弃所有的Variable Length Options。
* Rsvd.（6bit）：保留字段。
* Protocol Type（16bit）：被封装的协议类型，例如Ethernet就是0x6558。这个字段的存在，使得GENEVE封装其他的二层协议成为可能。
* VNI（24bit）：老朋友了。
* Reserved（8bit）：保留字段。Variable Length Options：由TLV构成，包含了可扩展的元数据。

## Links
1. [网络虚拟化协议GENEVE](https://zhuanlan.zhihu.com/p/35790366)
