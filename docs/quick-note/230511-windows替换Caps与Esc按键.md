# windows 下替换 Caps 与 Esc 按键
@Time("2023-05-11")

新建 .txt 文件，将下列代码复制粘贴到该文件中，并重命名为 .reg 格式文件。
```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout]
"Scancode Map"=hex:00,00,00,00,00,00,00,00,03,00,00,00,3a,00,01,00,01,00,3a,00,00,00,00,00
```

运行后重启即可

如果想要恢复默认同样新建 .txt 文件，将下列代码复制粘贴到该文件中，并重命名为 .reg 格式文件。
```
Windows Registry Editor Version 5.00
 
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout]
"Scancode Map"=-
```

当然对于这两个按键互换的需求我还看到有人推荐使用 Power Toys 的 Keyboard Manager ，或是 ahk 来实现的。我的评价是玩一玩可以如果真用还得是改注册表。
当然，我并不是说 Power Toys 和 ahk 不好，相反他们是十分的强大的效率必备工具，但他们很可能会在特定的环境下失效，这时你一定会高血压。
所以对于这种常用的，不用实现复杂功能的按键来说修改注册表是最好，最稳定的做法。

