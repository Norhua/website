# shell 编程

bash -n *.sh # 语法检查

## 变量

**变量赋值：**

```
name='value'
```

value 可以为：

```
直接字串：name='root'
变量引用：name="SUSER"
命令引用：name=`COMMAND` 或 name=$(COMMAND)
```

**变量引用：**

```
$name
${name}
```

弱引用和强引用

- "$name" 弱引用，其中的变量引用会被替换为变量值
- '$name'  强引用，其中的变量引用不会被替换为变量值，而保持原字符串

```bash
[amadeus@Admin ~]$ NUM='seq 10'
[amadeus@Admin ~]$ echo $NUM
seq 10
[amadeus@Admin ~]$ NUM=`seq 10`
[amadeus@Admin ~]$ echo $NUM
1 2 3 4 5 6 7 8 9 10
[amadeus@Admin ~]$ echo "$NUM"
1
2
3
4
5
6
7
8
9
10
```



### 只读变量

只读变量：只能声明定义，但后续不能修改和删除，即常量

声明只读变量：

```bash
readonly name
declare-r name
```

## 环境变量

环境变量：可以使子进程（包括孙子进程）继承父进程的变量，但是无法让父进程使用子进程的变量，一旦子进程修改从父进程继承的变量，将会新的值传递给孙子进程

变量声明和赋值：

```bash
#声明并赋值
export name=VALUE
declare-x name=VALUE

#或者分两步实现
name=VALUE
export name
```
### bash 内建的环境变量

```
PATH
SHELL
USER
UID
HOME
PWD
SHLVL	#she11的嵌套层数，即深度
LANGMAIL
HOSTNAME
HISTSIZE
_	#下划线，表示前一命令的最后一个参数
```


## 位置变量

位置变量：在 pash shell 中内置的变量，在脚本代码中调用通过命令行传递给脚本的参数

```
$1，$2，...对应第1个、第2个等参数，shift[n]换位置
$0	命令本身，包括路径
$*	传递给脚本的所有参数，全部参数合为一个字符串
$@	传递给脚本的所有参数，每个参数为独立字符串
$#	传递给脚本的参数的个数
注意：$@ $*只在被双引号包起来的时候才会有差异
```

清空所有位置变量

```bash
set -
```



![image-20221127121959752](images\image-20221127121959752.png)

![image-20221127122021818](images\image-20221127122021818.png)

![image-20221127122319463](images\image-20221127122319463.png)



![image-20221127123528312](images\image-20221127123528312.png)

![image-20221127123503631](images\image-20221127123503631.png)

![image-20221127123701206](images\image-20221127123701206.png)

![image-20221127123929162](images\image-20221127123929162.png)

## 算术运算

![image-20221127133331519](images\image-20221127133331519.png)
