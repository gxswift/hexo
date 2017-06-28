﻿---
title: lwip 配置
date: 2017-06-28 23:40:27
tags:
---


<!-- more -->  
#define SYS_LIGHTWEIGHT_PROT    		1							//为1时使用实时操作系统的轻量级保护,保护关键代码不被中断打断
#define NO_SYS                  		0  							//使用UCOS操作系统
#define MEM_ALIGNMENT           		4  							//使用4字节对齐模式
#define MEM_SIZE                		6*1024						//内存堆heap大小
#define MEMP_NUM_PBUF           		16							//MEMP_NUM_PBUF:memp结构的pbuf数量,如果应用从ROM或者静态存储区发送大量数据时,这个值应该设置大一点
#define MEMP_NUM_UDP_PCB        		5							//MEMP_NUM_UDP_PCB:UDP协议控制块(PCB)数量.每个活动的UDP"连接"需要一个PCB.
#define MEMP_NUM_TCP_PCB        		5							//MEMP_NUM_TCP_PCB:同时建立激活的TCP数量
#define MEMP_NUM_TCP_PCB_LISTEN 		6							//MEMP_NUM_TCP_PCB_LISTEN:能够监听的TCP连接数量
#define MEMP_NUM_TCP_SEG        		10							//MEMP_NUM_TCP_SEG:最多同时在队列中的TCP段数量
#define MEMP_NUM_SYS_TIMEOUT    		8							//MEMP_NUM_SYS_TIMEOUT:能够同时激活的timeout个数

//pbuf选项
#define PBUF_POOL_SIZE          		20							//PBUF_POOL_SIZE:pbuf内存池个数
#define PBUF_POOL_BUFSIZE     			512							//PBUF_POOL_BUFSIZE:每个pbuf内存池大小

#define LWIP_TCP                		1  							//使用TCP
#define TCP_TTL                			255							//生存时间

#undef TCP_QUEUE_OOSEQ
#define TCP_QUEUE_OOSEQ         		1 							//当TCP的数据段超出队列时的控制位,当设备的内存过小的时候此项应为0

#undef TCPIP_MBOX_SIZE
#define TCPIP_MBOX_SIZE         		MAX_QUEUE_ENTRIES   		//tcpip创建主线程时的消息邮箱大小

#undef DEFAULT_TCP_RECVMBOX_SIZE
#define DEFAULT_TCP_RECVMBOX_SIZE       MAX_QUEUE_ENTRIES  

#undef DEFAULT_ACCEPTMBOX_SIZE
#define DEFAULT_ACCEPTMBOX_SIZE         MAX_QUEUE_ENTRIES  

		
#define TCP_MSS                			(1500 - 40)	  				//最大TCP分段,TCP_MSS = (MTU - IP报头大小 - TCP报头大小
#define TCP_SND_BUF            		 	(2*TCP_MSS)					//TCP发送缓冲区大小(bytes).
#define TCP_SND_QUEUELEN       		 	(4* TCP_SND_BUF/TCP_MSS)	//TCP_SND_QUEUELEN: TCP发送缓冲区大小(pbuf).这个值最小为(2 * TCP_SND_BUF/TCP_MSS)
#define TCP_WND               		  	(2*TCP_MSS)					//TCP发送窗口
#define LWIP_ICMP             		  	1 							//使用ICMP协议
#define LWIP_DHCP             		  	1							//使用DHCP
#define LWIP_UDP              		  	1 							//使用UDP服务
#define UDP_TTL               		  	255 						//UDP数据包生存时间
#define LWIP_STATS 						0
#define LWIP_PROVIDE_ERRNO 				1


#define LWIP_NETCONN                    1 							//LWIP_NETCONN==1:使能NETCON函数(要求使用api_lib.c)
#define LWIP_SOCKET                     1							//LWIP_SOCKET==1:使能Sicket API(要求使用sockets.c)
#define LWIP_COMPAT_MUTEX               1		
#define LWIP_SO_RCVTIMEO                1 							//通过定义LWIP_SO_RCVTIMEO使能netconn结构体中recv_timeout,使用recv_timeout可以避免阻塞线程

//有关系统的选项
#define TCPIP_THREAD_PRIO				5							//定义内核任务的优先级为5
#define TCPIP_THREAD_STACKSIZE          1000						//内核任务堆栈大小
#define DEFAULT_UDP_RECVMBOX_SIZE       2000
#define DEFAULT_THREAD_STACKSIZE        512

//LWIP调试选项
#define LWIP_DEBUG                    	0	 						//关闭DEBUG选项
#define ICMP_DEBUG                     	LWIP_DBG_OFF 				//开启/关闭ICMPdebug