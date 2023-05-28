# 文件管理器 pcmanfm

## 基础安装 (ArchLinux)
```shell
sudo pacman -S pcmanfm
```

## 必要功能
如果你使用的是 WM ，那么你还需要 gvfs 来使 pcmanfm 可以识别设备。如果你还需要自动挂载那么你还需要 udisks2 。
```
sudo pacman -S gvfs
sudo pacman -S udisks2
sudo systemctl enable udisks2
```

## 配置 pcmanfm 为默认文件管理器
在使用的过程中我发现在使用一些应用中的“在文件夹打开”功能时无法找到 pcmanfm 从而使用其他软件打开的，
比如 linuxqq 就会用 vscode 打开
编辑 ~/.local/share/applications/mimeapps.list 文件， 添加
```
[Default Applications]
inode/directory=pcmanfm.desktop
```
这样就把 pcmanfm 设置为默认文件管理器了。

> 全文参考：
> https://wiki.archlinux.org/title/PCManFM
> https://wiki.archlinux.org/title/File_manager_functionality

