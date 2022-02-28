# Data structure

## IP


### iphdr

```c
struct iphdr {
#if defined(__LITTLE_ENDIAN_BITFIELD)
	__u8	ihl:4,
		version:4;
#elif defined (__BIG_ENDIAN_BITFIELD)
	__u8	version:4,
  		ihl:4;
#else
#error	"Please fix <asm/byteorder.h>"
#endif
	__u8	tos;
	__be16	tot_len;
	__be16	id;
	__be16	frag_off;
	__u8	ttl;
	__u8	protocol;
	__sum16	check;
	__be32	saddr;
	__be32	daddr;
	/*The options start here. */
};
```

* `iphdr->ihl`: 首部长度(4位):首部长度指的是IP层头部占32 bit字的数目(也就是IP层头部包含多少个4字节 -- 32位),包括任何选项。由于它是一个4比特字段,因此首部最长为60个字节。普通IP数据报(没有任何选择项)字段的值是5 <==> 5 * 32 / 8 = 5 * 4 = 20 Bytes

Links:

1. [struct iphdr详解](https://blog.csdn.net/beginning1126/article/details/14057087)


## TCP

### tcphdr


```c
struct tcphdr {
    __be16 source;
    __be16 dest;
    __be32 seq;
    __be32 ack_seq;
#if defined(__LITTLE_ENDIAN_BITFIELD)
    __u16   res1:4,
            doff:4,
            fin:1,
            syn:1,
            rst:1,
            psh:1,
            ack:1,
            urg:1,
            ece:1,
            cwr:1;
#elif defined(__BIG_ENDIAN_BITFIELD)
    __u16   doff:4,
            res1:4,
            cwr:1,
            ece:1,
            urg:1,
            ack:1,
            psh:1,
            rst:1,
            syn:1,
            fin:1;
#else
#error "Adjust your <asm/byteorder.h> defines"
#endif
    __be16 window;
    __be16 check;
    __be16 urg_ptr;
};
```

![tcp header](https://img2018.cnblogs.com/blog/1241434/201910/1241434-20191014094711064-1041986148.png)

Links:

1. [tcphdr](https://docs.huihoo.com/doxygen/linux/kernel/3.7/structtcphdr.html)
2. [struct tcphdr解析](https://www.cnblogs.com/wanghao-boke/p/11669744.html)


### CONNECTION

Links:

1. [理解TCP序列号（Sequence Number）和确认号（Acknowledgment Number）](https://xzchsia.github.io/2020/08/31/tcp-seq-ack/)


## UDP

### udphdr
```c
struct udphdr {
        __u16   source;
        __u16   dest;
        __u16   len;
        __u16   check;
 };
```

Links:

1. [struct udphdr](https://www.cnblogs.com/wanghao-boke/p/11669824.html)
