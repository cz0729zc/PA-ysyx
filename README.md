# PA-学习日志

## Day1

### 总体

将Linux安装在虚拟机中，系统为**ubuntu-22.04.3-desktop-amd64**，并且成功配置清华源，安装相应软件,[学习了github](https://zhuanlan.zhihu.com/p/369486197)以及[git](https://blog.csdn.net/qq_37772475/article/details/107140061)，和vim[的使用方法](https://zhuanlan.zhihu.com/p/68111471)

### 问题

1.Linux下切换root用户提示**Authentication failure**

2.下载vim时出现以下问题

~~~
下列软件包有未满足的依赖关系：
 vim : 依赖: vim-common (= 2:8.2.3995-1ubuntu2) 但是 2:8.2.3995-1ubuntu2.10 正要被安装
E: 无法修正错误，因为您要求某些软件包保持现状，就是它们破坏了软件包间的依赖关系。
~~~

3.使用git clone远端仓库时出现以下问题

```
$  Git clone https://github.com/cz0729zc/PA-ysyx.git
Cloning into 'PA-ysyx'...
fatal: unable to access 'https://github.com/cz0729zc/PA-ysyx.git/': Failed to connect to github.com port 443 after 21088 ms: Couldn't connect to server
```

4.对git branch 之间的关系有了更深入的了解：在分支下创建文件后，需要对其add和commit。

### 解决方法及原因

问题一：[解决方法](https://blog.csdn.net/renrenxu/article/details/82725659)

问题二：[解决方法](https://blog.csdn.net/qq_40748967/article/details/122040610)

问题三：[解决方法](https://zhuanlan.zhihu.com/p/636418854)

问题四：[解决方法](https://zhuanlan.zhihu.com/p/410255613)
