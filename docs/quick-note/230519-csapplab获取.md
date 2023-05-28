# csapp lab 获取与一些配置

## 获取
访问 [CSAPP 官网](http://csapp.cs.cmu.edu/3e/students.html)
找到 [Labs for self-study students (without solutions)](http://csapp.cs.cmu.edu/3e/labs.html) 页面即可下载 lab 相关文件
在这个页面中列出了所有的 lab 与其相关的文件的下载连接， 其中:

- README: lab 介绍 ( 必读 )
- Writeup: 应该也是 lab 介绍
- Release Notes: 发行版本说明
- Self-Stidy Handout: lab 代码 

## 解压
以 datalab 为例，使用 tar 命令解开存档
```shell
tar -xvf datalab-handout.tar
```
在这些 tar 存档中有一些二进制可执行文件，如果你使用其他方式解包，这些文件可能会失去相应的权限
这时你可能需要手动给予权限才能使实验正常进行
还是以 datalab-handout 下的文件举例
```shell
chmod +x dlc driver.pl
```

