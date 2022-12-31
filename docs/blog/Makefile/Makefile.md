# Makefile

## 0xff 为什么要学 Makefile

因为做 pa 需要



## 0x01 初识Makefile

make常用选项

make \[-f file\]\[options\]\[target\]

Make默认在当前目录中寻找GUNmakefile，makelfile，Makefile的文件作为make的	输入文件

-f   	 	千可以指定除上述文件名之外的文件作为输入文件

-V  	 	显示版本号-n只输出命令，但并不执行，一般用来测试

-s  	 	只执行命令，但不显示具体命令，此处可在命令中用@符抑制命令输出

-w 	 	显示执行前执行后的路径

-C dir	 指定makefile所在的目录

没有指定目标时，默认使用第一个目标



Makefile基本格式

```makefile
目标a:a依赖
	命令a
目标b:b依赖
	命令b
...
```

当使用 make 目标x 生成 目标x 时make会先生成该目标的所有依赖，当只执行 make 时默认生成第一个目标。



## 0x02 使用make减少不必要的编译

在多文件编译的过程中我们通常这样编译

```shell
 ~/test/make  ls
add.c  add.h  calc.c  Makefile  mult.c  mult.h  sub.c  sub.h
 ~/test/make  gcc add.c sub.c mult.c calc.c -o cala
```

这样每次编译时都会重新编译所有文件浪费时间，对于没有修改过的源文件我们没有必要重新编译

所以我们可以使用make管理

```makefile
cala:add.o sub.o mult.o
        gcc add.o sub.o mult.o calc.c -o calc
add.o:add.c
        gcc -c add.c -o add.o
sub.o:sub.c
        gcc -c sub.c -o sub.o
mult.o:mult.c
        gcc -c mult.c -o mult.o

clean:
        rm -rf *.o *.out cala
```



## 0x03 Makefile 中的变量

系统变量

​	\$* 不包括扩展名的目标文件名称

​	\$+ 所有的依赖文件，以空格分隔

​	\$< 表示规则中的第一个条件

​	\$？所有时间戳比目标文件晚的依赖文件，以空格分隔

​	\$@ 目标文件的完整名称 

​	\$^ 所有不重复的依赖文件，以空格分隔

​	\$% 如果目标是归档成员，则该变量表示目标的归档成员名称

系统常量(可用 meke -p 查看)

​	AS	  汇编程序的名称        默认 as 

​	CC      C编译器名称             默认 cc

​	CPP    C预编译器名称         默认 cc -E 

​	CXX    C++编译器名称         默认 g++

​	RM     文件删除程序别名    默认 rm -f

自定义变量

​	定义：变量名=变量值

​	使用：\$(变量名) 或 \${变量名}

```makefile
OBJ=add.o sub.o mult.o calc.o # 设置自定义变量
TARGET=calc

$(TARGET):$(OBJ)
        gcc $(OBJ) -o $(TARGET)

add.o:add.c	
		# 这里使用系统常量 CC 替代 gcc 提高跨平台性与灵活性
        $(CC) -c $^ -o $@ # 使用系统变量替代命令内容
sub.o:sub.c
        $(CC) -c $^ -o $@
mult.o:mult.c
        $(CC) -c $^ -o $@
calc.o:calc.c
        $(CC) -c $^ -o $@

clean:
        $(RM) *.o *.out $(TARGET)
```



## 0x04 伪目标与模式匹配

伪目标

```makefile
.PHONY:clean
```

声明目标为伪目标之后，makefile将不会判断目标是否存在或该目标是否需要更新

%.o:%.cpp		.o依赖于对应的.cpp

wildcard	 \$(wildcard./\*.cpp)获取当前目录下所有的.cpp文件*

patsubst 	\$(patsubst %.cpp, %.o, ./\*.cpp)将对应的cpp文件名替换成.o文件名



```makefile
OBJ=$(patsubst %.c, %.o, $(wildcard ./*.c))
TARGET=calc

$(TARGET):$(OBJ)
        gcc $(OBJ) -o $(TARGET)

%.o:%.c	
        $(CC) -c $^ -o $@

clean:
        $(RM) *.o *.out $(TARGET)
.PHONY:clean
```

