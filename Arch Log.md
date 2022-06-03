# Arch Linux 安装过程中遇到问题的解决


### go 语言 proxy.golang.org timeout 无法访问 处理方法

处理方法：换一个国内能访问的代理地址：https://goproxy.cn
```
go env -w GOPROXY=https://goproxy.cn
```