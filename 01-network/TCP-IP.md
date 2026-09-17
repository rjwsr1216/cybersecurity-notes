# TCP/IP 学习笔记

## 1. TCP 是什么？

TCP（Transmission Control Protocol）
是一种面向连接、可靠的传输层协议。

## 2. TCP 的主要特点

- 面向连接
- 可靠传输
- 有序传输
- 流量控制
- 拥塞控制

## 3. TCP 三次握手

客户端首先发送 SYN。

服务器收到后返回 SYN + ACK。

客户端收到后发送 ACK。

连接建立。

## 4. 网络安全中的意义

理解 TCP 是学习网络安全的基础。

后续需要继续学习：

- SYN Flood
- TCP Reset
- TCP 会话
- Wireshark 抓包
- TCP/IP 协议分析

## 5. 我的疑问

为什么 TCP 需要三次握手？

为什么不能两次握手？

SYN Flood 是如何利用 TCP 三次握手的？
