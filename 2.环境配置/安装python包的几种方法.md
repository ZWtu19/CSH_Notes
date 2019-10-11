#### 安装Python包的几种方法总结(需要使用termial工具\git工具)

##### 包管理方法原理
![Python包管理说明](https://img-blog.csdnimg.cn/20190710142826527.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTMwOTUzMzM=,size_16,color_FFFFFF,t_70)

##### 通过pip安装（首选）
_使用pip安装的格式_ 
```shell script
pip install 包名
```

* 注意在某些情况下提示找不到适合当前版本的错误提示后，可能需要修改镜像，格式如下：  
```shell script
# 注意两个镜像地址有细微差异，详见https://www.jb51.net/article/159167.htm
pip install 包名 -i 镜像地址1 --trusted-host 镜像地址2

```

##### 通过pypi安装（备选）
_使用pypi安装的格式_  
```shell script
# 需要使用setup.py,故需要进入setup.py的目录下，或者配置环境变量
# 类似于win下的安装引导
python setup.py install 包名
```

##### 通过源码安装

_下载源码文件并安装，常见格式为msi、exe、tar.gz（由于系统不同格式不同_)

##### 若使用的是python的发行版，以anaconda为例
安装格式为： 
```shell script
conda install <包名>
```

