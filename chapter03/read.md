# 第3章--套接字编程简介  
## 3.1 套接字地址结构  
大多数套接字都需要一个指向套接字地址结构的指针作为参数。每个协议族都定义它自己的套接字地址。这些结构的名字均以sockaddr_开头，并以对应每个协议族的唯一后缀结尾  

IPv4套接字地址结构：  
命名：sockaddr_in  
定义：<netinet/in.h>  
struct in_addr{  
    in_addr_t s_addr; /* 32位IP地址 */  
};  

struct sockaddr_in{  
    uint8_t sin_len: /* 地址长度（字节数） */;  
    sa_family_t sin_family: /* 地址族 */;  
    in_port_t sin_port: /* 端口 */;  
    struct in_addr sin_addr: /* IP地址 */;  
    char sin_zero[8]: /* 未用 */;  
};  


通用套接字地址结构：  
定义：<sys/socket.h>  
struct sockaddr{  
    uint8_t sa_len: /* 地址长度（字节数） */;  
    sa_family_t sa_family: /* 地址族 */;  
    char sa_data[14]: /* 协议特定的地址 */;  
};  


IPv6套接字地址结构：  
定义：<netinet/in.h>  
struct in6_addr{
    uint8_t s6_addr[16]; /* 128位IP地址 */  
}  
struct sockaddr_in6{  
    uint8_t sin6_len: /* 地址长度（字节数） */;  
    sa_family_t sin6_family: /* 地址族 */;  
    in_port_t sin6_port: /* 端口 */;  
    uint32_t sin6_flowinfo: /* 流信息 */;  
    struct int6_addr sin6_addr: /* IP地址 */;  
    uint32_t sin6_scope_id: /* 接口 */;  
}  

## 3.2 值-结果函数  
1. 从进程到内核传递套接字地址结构的函数有3个：bind, connect, sendto  
2. 从内核到进程传递套接字地址结构的函数有4个：accept, recvfrom, getsockname, getpeername  

## 3.5 inet_aton,inet_addr, inet_ntoa函数  
- inet_aton, inet_addr, inet_ntoa函数处理点分十进制数串和IPV4网络字节二进制序之间转换  
- inet_pton, inet_ntop函数处理二进制序IPv6和IPv4都适合  

## 3.6 inet_pton, inet_ntop函数


## 3.7 sock_ntop和相关函数  
#include "unp.h"  
char *sock_ntop(const struct sockaddr *sockaddr, socklen_t addrlen);  
//若成功则为非空指针，若出错则为NULL  

## 3.8 readn,writen,readline函数  
