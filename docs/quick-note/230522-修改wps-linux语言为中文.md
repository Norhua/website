# 修改 wps-linux 语言为中文

最近把设置在 .zshrc 的中文本地化设置取消了，然后我用的国际版 wps 就直接显示英文了
然后我又没有在 wps 设置里找到语言的选项，网上查了一下发现原本在一个地方有设置按钮但现在没了。

## 通用方案
不建议在 /etc/locale.conf 中设置全球中文区域设置，因为这会导致tty显示乱码。
您可以在 ~/.bashrc 、 ~/.xinitrc 或 ~/.xprofile 中设置自己的用户环境变量。
```
export LANG=zh_CN.UTF-8
export LANGUAGE=zh_CN:en_US
```
> 参考
> https://wiki.archlinux.org/title/Localization/Simplified_Chinese

## 只设置 wps 为中文
编辑sudo vim /usr/bin/wps
```shell
sudo vim /usr/bin/wps
```
在文件最开头加上如下两行
```
export LANG=zh_CN.UTF-8
export LANGUAGE=zh_CN:en_US
```
