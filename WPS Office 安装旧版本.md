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

---

## 如果又想用其他新版本的wps套件怎么办？

我没找到把新旧版本混在一直的方法，因此保留了两个版本，只用旧版本的wpspdf

4. 复制`/usr/lib/office6`文件夹到其他目录（放软件的目录，或者直接改名为`office6_old`）

5. 从aur更新wps到最新版本

6. 修改`/usr/bin/wpspdf`，注释掉里面的内容，写入第四步复制的`office6_old`的路径，例如：
    ```
    /usr/lib/office6_old/wpspdf
    ```
