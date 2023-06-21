---
title: HTTP
date: 2023-05-11 20:45:05
tags: web
---

# 一、概述
HTTP 超文本传输协议
HyperText Transfer protocol

### 基本性质
- 简约的
- 可扩展的
- 无状态，但并非无会话（HTTP Cookie）
- 和网络连接

### 能控制的特性
- 缓存
- 开放同源限制
- 认证（WWW-Authenticate或HTTP cookie）
- 代理服务器和隧道（SOCKs，ftp）
- 会话

# 二、报文
### 请求 Request

```
GET / HTTP/1.1
Host:developer.mozilla.org
Accept-Language:fr
```
**起始行**
- `GET` 请求方法
- `/` 路径，请求目标（URL、协议、端口和域名的绝对路径）
- `HTTP/1.1` 协议版本

**标头**
`Host ... :fr` 标头(Headers)
- 通用标头，适用于整个消息
- 请求标头
- 表示标头

**主体（Body）**
将数据发送到服务器以便更新数据，POST请求（包含HTML表单数据）
- 单一资源
- 多资源

### 响应 Response
```
HTTP/1.1 200 OK
Date:Sat,09 Oct 2010 15:30:01 GMT
Last-Modified:Tue, 01 Dec 2009 20:15:22 GMT
ETag:"51142bc1-7449-479b075b2891b"
Accept-Ranges:bytes
Content-Length:29769
Content-Type:text/html
```
**状态行**
- `HTTP/1.1` 协议版本
- `200` 状态码
- `OK` 信息状态/状态文本

**标头**

**主体**

### 状态响应码
