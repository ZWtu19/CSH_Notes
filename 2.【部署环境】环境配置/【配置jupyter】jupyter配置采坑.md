#### 一、安装
##### （一）安装jupyter lab
* 通过终端命令即可实现安装

```bash
pip install jupyterlab
```
##### （二）依赖安装
* 安装Nodejs

```bash
# 首先安装conda，需要下载对应操作系统的可执行文件，并执行
wget XXXXX_x64.sh
bash ./XXXXXX_x64.sh

# 通过conda安装nodejs
conda install -c conda-forge nodejs
```
* 一般正常安装后，通过命令：jupyter lab即可访问
##### （三）插件安装
* 进入jupyter lab后，需要点击setting->Enable Extension Manager，激活插件管理器
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200828151717674.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70#pic_center)
* 点击插件管理器，搜索感兴趣的插件，选择`install`，即可实现安装插件，安装成功后即可看到已安装的插件信息
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020082815192410.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70#pic_center)
* 插件安装情况查看：可在本机终端或jupyter lab终端通过命令查看安装信息

```bash
# 在终端中输入命令即可查看
jupyter labextension list
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200828152242416.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70#pic_center)
* 插件推荐：[15款好用的插件推荐](https://zhuanlan.zhihu.com/p/101070029)

#### 二、配置
##### （一）可配置远程访问服务
* 可配置远程服务
* 详细信息可参考[内网穿透+jupyter](https://github.com/ZWtu19/Notes/blob/master/2.%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE/%E5%86%85%E7%BD%91%E7%A9%BF%E9%80%8F%2Bjupyter%E6%9C%8D%E5%8A%A1.md)
* 实现效果如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200828152650354.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70#pic_center)
##### （二）添加常用插件
* github
* toc
* drawio
* 其他
#### 四、调试
##### （一）插件无法使用/加载失败
* 这类情况常常出现于卸载、重装插件的情况；
* 首先通过命令jupyter labextension list 查看安装的插件是否同时出现在`installed`和`uninstalled`下；
* 如果同时出现，可删除配置文件并重启服务：

	`rm '你的env路径'/share/jupyter/lab/settings/build_config.json`

##### （二）无法指定虚拟环境
在完成jupyter lab的安装和配置后，实际运行代码时，发现无法指定某一虚拟环境：
* 可通过命令，进入某一虚拟环境， 并使用jupyter lab

```bash
# 进入某虚拟环境
conda activate Usual
# 进入jupyter lab
jupyter lab
```
* 可直接指定虚拟环境

```bash
# 安装nb_conda包
conda install nb_conda ipykernel
# 指定虚拟环境
ipython kernel install --user --name ‘虚拟环境名’
```
* 成功配置后的新建文件页面
![在这里插入图片描述](https://img-blog.csdnimg.cn/202008281540254.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70#pic_center)
* 成功配置后的选择内核界面
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020082815405370.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70#pic_center)

