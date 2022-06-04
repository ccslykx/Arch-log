# Arch Linux 安装过程中遇到问题的解决


### go 语言 proxy.golang.org timeout 无法访问 处理方法

处理方法：换一个国内能访问的代理地址：https://goproxy.cn
```
go env -w GOPROXY=https://goproxy.cn
```

### 安装Windows字体

复制Windows的字体文件到`/usr/share/fonts/Winfonts/`下，删除`.fon`文件，保留`.ttf`和`.ttc`文件，然后：
```
sudo mkfontscale
sudo mkfontdir
fc-cache -fv
```

### RStudio 启动白屏

**解决办法** 在`/usr/share/applications/rstudio.desktop`中加入启动参数： `-no--sandbox`