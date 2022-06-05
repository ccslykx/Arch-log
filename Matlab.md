# 下载安装
## 下载
[百度网盘(Matlab R2019b Linux)](https://pan.baidu.com/s/1I4mc4eQtvn5ZATjgg8rFaQ?pwd=iyka)

下载其中的两个文件，一个是安装镜像，另一个是破解文件
## 安装
### 挂载
```bash
sudo mkdir /mnt/matlab
mount ./R2019b_Linux.iso /mnt/matlab
```
### 安装
```bash
sudo /mnt/matlab/install
```
选择离线激活，然后开始安装，需要序列号时输入序列号

`09806-07443-53955-64350-21751-41297`
> 如果安装界面有中文显示不正常，可以先不去管，等到安装完成再去处理

## 破解
解压`Matlab R2019b Linux64 Crack.tar.gz`,找到`license_standalone.lic`文件

更改权限
```bash
sudo chmod 777 ./license_standalone.lic
```
复制破解文件
```bash
sudo mkdir 安装目录/licenses
sudo cp ./license_standalone.lic 安装目录/licenses/
sudo cp -r ./R2019b/bin 安装目录/
```
### 尝试运行
```bash
安装目录/bin/matlab
```
此时会报错
```
MATLAB is selecting SOFTWARE OPENGL rendering.                            
/opt/matlab/bin/glnxa64/MATLAB: error while loading shared libraries: libcrypt.so.1: cannot open shared object file: No such file or directory
```
根据[Mathworks](https://www.mathworks.com/matlabcentral/answers/473294-why-do-i-see-the-error-error-while-loading-shared-libraries-libcrypt-so-1-when-starting-matlab-on)的解答，需要安装`libxcrypt-compat`软件包，原本这一软件包在AUR,现在AUR已经搜不到这个包了，可以直接在官方仓库安装。
```bash
sudo pacman -S libxcrypt-compat
```
安装成功之后，再次尝试打开，即可正常启动了。
## 添加应用程序图标
matlab不会自动创建应用程序图标，需要手动创建

在`/usr/share/applications/`目录下创建`matlab.desktop`文件，写入以下内容：
```desktop
[Desktop Entry]
Type=Application
Terminal=false
MimeType=text/x-matlab
Exec=安装目录/bin/matlab -desktop
Name=MATLAB
Icon=matlab
Categories=Development;Math;Science
Comment=Scientific computing environment
StartupNotify=true
```
保存退出就可以看到创建了应用程序图标

## 解决常见问题
### 中文字体
遇到matlab中文显示异常，一般是字体的问题，参考[matlab 汉字是方块,linux下Matlab 2020中文字体方框问题解决方法](https://blog.csdn.net/weixin_30588427/article/details/115879282)解决

下载支持中文的等宽字体
[Consolas-with-Yahei](https://github.com/crvdgc/Consolas-with-Yahei)
安装为系统字体，实测直接在matlab设置中切换为该字体之后重启即可，如果不行再根据[matlab 汉字是方块,linux下Matlab 2020中文字体方框问题解决方法](https://blog.csdn.net/weixin_30588427/article/details/115879282)步骤来操作

### 菜单栏缩放
在高分屏下，菜单栏字体很小，看起来很难受，可以根据[解决Ubuntu高分屏下matlab标题栏（菜单栏）字体过小问题](https://blog.csdn.net/zwhut/article/details/79779174)提供的方法来解决

在matlab中的命令行窗口执行如下两条命令
```matlab
s = settings;s.matlab.desktop.DisplayScaleFactor
s.matlab.desktop.DisplayScaleFactor.PersonalValue = 1.5
```
> 最后的1.5是缩放倍数，可以根据实际情况进行调节

重启matlab之后可以看到，缩放变得正常了。

### Simulink启动报错
报错信息：
```
警告: MATLABWindow 应用程序未能启动。Unable to
launch the MATLABWindow application 
> In sltemplate.ui/StartPage/showWithFallback
  In sltemplate.ui/StartPage/show
```

参考[Why is MATLAB unable to run the MATLABWindow application on Linux?](https://www.mathworks.com/matlabcentral/answers/364551-why-is-matlab-unable-to-run-the-matlabwindow-application-on-linux)提供的解决方案

在matlab命令行中执行

```matlab
cd(matlabroot)
! bin/glnxa64/MATLABWindow
```

查看报错信息，根据报错信息分别处理

如：

```matlab
bin/glnxa64/MATLABWindow: path to/libstdc++.so.6: version `CXXABI_1.3.9' not found (required by _somelibrary_)
```

看到形如这样的报错，就需要去`安装目录/sys/os/glnxa64`目录下去处理`libstdc++.so.6`文件

具体操作如下：

```bash
cd 安装目录/sys/os/glnxa64
sudo mkdir exclude
sudo mv libstdc++.so.6* exclude/
```

如此反复测试，根据文章内容列出的几种情况分别处理，知道不再报错即可。

> 注意，不同情况需要处理的库文件在不同的目录，要仔细阅读注意分辨。

## 完结撒花

至此matlab基本功能均可正常使用。
