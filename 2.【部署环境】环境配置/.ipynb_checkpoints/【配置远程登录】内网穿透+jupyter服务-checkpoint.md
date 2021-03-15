### 一、内网穿透
#### （一）内网穿透说明
* 内网穿透的理解涉及到计算机网络原理的相关知识，若感兴趣可移步别处了解
* 内网穿透一般用于以下状况

| 需求场景 | 说明 |
|--|--|
| 在外网访问内网(局域网)内的服务或程序 | 有需求 |
| 与甲方交接时使用Demo，有站点需求 | 有需求 |
| 做微信、支付宝等第三方平台的接口服务时，未使用外网回调地址 | 开发需求 |
* 以本人为例，服务器部署在实验室，出差在外即无法使用服务器的资源，较为不便，使用内网穿透，即可突破局域网的限制，联网即可访问内网服务器，完成学习任务和工作
#### （二）内网穿透工具
* 常见内网穿透工具

|工具|说明|
|--|--|
|Ngrok|免费，老牌强大的穿透工具，开源，源码很久未更新了|
|钉钉穿透|免费，基于Ngrok封装，简单快速，适合新手和个人开发者|
|花生壳|收费，需要注册账号，并进行实名认证，注册流程较长，可自选域名，有流量限制|
|NATAPP|免费通道：http，tcp，ucp全通道穿透，域名随机；收费通道：不限流量，域名自选；|
|FRP自建|要求自建的云服务器、域名，带宽取决于云服务器；适合企业开发使用，可穿透任意合法端口|

* 其他穿透工具
### 二、钉钉内网穿透
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200826153412245.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70#pic_center)
### 三、服务器端配置
#### （一）环境安装
* git安装

```shell
pip install git
```

* jupyter安装
```shell
pip install jupyter
```
* 其他工具安装
#### （二）jupyter配置
* 要求已安装python、ipython、jupyter，请自行安装
* 新建jupyter notebook配置文件

```shell
# 生成~/.jyupyter/jupyter_notebook_config.py配置文件
jupyter notebook --generate-config  
```
* 通过ipython查看密码
```shell
ipython
```
```python
from notebook.auth import passwd
# 生成并输出密码
passwd()
```
* 编辑配置文件

```bash
vim ~/.jupyter/jupyter_notebook_config.py
```

```bash
c.NotebookApp.ip='*'
c.NotebookApp.password = u'生成的密码' #将输出的密码黏贴至绿色文字处
c.NotebookApp.open_browser = False # 默认在本地不打开浏览器
c.NotebookApp.port =8888 # 设置服务端口
```
* 保存并退出配置文件
* 测试（通过ip地址访问）
1. 同一局域网下：连接成功

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020082615465784.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70#pic_center)

3. 非同一局域网下：连接失败 -> 配置内网穿透，实现在非同一局域网下访问服务

#### （三）钉钉穿透配置
* 下载git包：[链接地址](https://github.com/open-dingtalk/pierced.git)

```bash
# clone项目到本地
git clone https://github.com/open-dingtalk/pierced.git
```

* 文件结构

|一级目录|二级目录|三级目录（可执行文件）|
|--|--|--|
|pierced|lnux|ding、ding.cfg|
|  |mac_64|ding、ding.cfg|
|  |windows_64|ding、ding.cfg|

* 根据服务器的系统，进入linux/mac_64/windows_64目录下，并执行可执行文件ding：
```shell
# 进入文件下载地址
cd ~/Downloads/pierced/
# linux
cd linux/
#./ding -config=./ding.cfg -subdomain=自定义域名 对外端口号
./ding -config=./ding.cfg subdomain csh_ubuntu 8888

# mac
cd mac_64/
#./ding -config=./ding.cfg -subdomain=自定义域名 对外端口号
./ding -config=./ding.cfg subdomain csh_ubuntu 8888

# windows
cd windows_64/
#./ding -config=./ding.cfg -subdomain=自定义域名 对外端口号
ding -config=ding.cfg subdomain csh_ubuntu 8888
```
* 等待执行结果，若出现以下截图，则说明穿透成功（注意forwarding对应的即为穿透后的网址和原地址）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200826151459560.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70#pic_center)

* 若以上截图中“Tunnel Status”不为online，则表示当前域名已存在，则需要重新设置domain，可重复执行ding命令，更改域名，直至成功

* 随便使用一台联网设备，通过域名访问服务，检查是否成功
1. 电脑
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200826151839977.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70#pic_center)
2. 手机
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200826152001305.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70#pic_center)
### 四、配置完成
* 其他服务也可通过类似方法完成，只需要指定正确的服务端口即可
