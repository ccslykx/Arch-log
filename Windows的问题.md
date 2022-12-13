# Windows的问题

## 修复蓝屏错误"0xc000000e"

1. 下载并安装`Windows ADK`与`Windows ADK的Windows PE加载项`。
2. 以管理员身份运行部署和映像工具环境
    ```cmd
    copype amd64 E:\WinPE_amd64 #复制amd64的PE相关文件到E盘
    MakeWinPEMedia /ISO E:\WinPE_amd64 E:\WinPE_amd64.iso #创建PE系统的iso文件
    ```
3. 使用rufus烧录系统到u盘
4. 从u盘启动PE系统
    ```cmd
    diskpart #进入DISKPART
    list vol #查看卷标，找到EFI分区
    #如果 EFI没有卷标
    select vol 0 #假如EFI分区是volume0
    assgin letter=E: #分配盘符E,E应该为未分配盘符
    #果如
    exit #退出DISKPART
    
    bcdboot c:\windows /s E: /f UEFI #修复引导
    ```
5. 重启即可

## 在arch linux下为grub添加windows引导

1. 终端执行以下命令并记录结果，命令末尾的路径（`bootmgfw.efi`的路径）根据自己情况修改：
    ```bash
    sudo grub-probe -t hints_string /efi/EFI/Microsoft/Boot/bootmgfw.efi
    sudo grub-probe -t fs_uuid /efi/EFI/Microsoft/Boot/bootmgfw.efi
    ```

2. 在`/boot/grub/grub.cfg`中添加，其中`search --fs-uuid --set=root`后的内容为上述命令得到的结果。
    ```
    menuentry "Windows" {
            insmod part_msdos
            insmod ntfs
            insmod search_fs_uuid
            insmod chain
            search --fs-uuid --set=root --hint-bios=hd0,gpt1 --hint-efi=hd0,gpt1 --hint-baremetal=ahci0,gpt1 194D-9D36
            chainloader /EFI/Microsoft/Boot/bootmgfw.efi
    }
    ```

3. 重启即可