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

### RStudio 

#### 启动白屏

**解决办法** 在`/usr/share/applications/rstudio.desktop`中加入启动参数： `-no--sandbox`

#### 无法使用输入法

`paru rstudio-fcitx5`

### 无法连接蓝牙耳机

安装 `pulseaudio-bluetooth` 。

### 更新报签名错误

```
错误：lame: 来自 "David Runge <dvzrv@archlinux.org>" 的签名是勉强信任的
:: 文件 /var/cache/pacman/pkg/lame-3.100-4-x86_64.pkg.tar.zst 已损坏 (无效或已损坏的软件包 (PGP 签名)).
打算删除吗？ [Y/n] y
错误：ostree: 来自 "David Runge <dvzrv@archlinux.org>" 的签名是勉强信任的
:: 文件 /var/cache/pacman/pkg/ostree-2022.5-1-x86_64.pkg.tar.zst 已损坏 (无效或已损坏的软件包 (PGP 签名)).
打算删除吗？ [Y/n] y
错误：telegram-desktop: 来自 "Jiachen YANG (Arch Linux Packager Signing Key) <farseerfc@archlinux.org>" 的签名是勉强信任的
:: 文件 /var/cache/pacman/pkg/telegram-desktop-4.0.2-4-x86_64.pkg.tar.zst 已损坏 (无效或已损坏的软件包 (PGP 签名)).
打算删除吗？ [Y/n] y
错误：无法提交处理 (无效或已损坏的软件包)
发生错误，没有软件包被更新。
```

解决：
```
sudo pacman -S archlinux-keyring
```