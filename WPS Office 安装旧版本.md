# WPS Office 安装旧版本

1. 从aur克隆`wps-office.git`
    ```
    git clone https://aur.archlinux.org/wps-office.git
    ```

2. 找到要安装历史版本的`提交ID`并恢复历史版本
    ```
    cd wps-office
    git reset --hard 74dc33e757b953b2f897d21b12dc653d1f314139
    ```

3. 执行`makepkg`并安装目录下的的`*.pkg.tar.zst`软件包
    ```
    makepkg

    sudo pacman -U wps-office-11.1.0.10161-1-x86_64.pkg.tar.zst
    sudo pacman -U wps-office-mime-11.1.0.10161-1-x86_64.pkg.tar.zst
    ```