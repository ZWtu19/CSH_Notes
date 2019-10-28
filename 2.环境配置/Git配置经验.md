#### 搭建Git环境
![git介绍](https://images2018.cnblogs.com/blog/628084/201807/628084-20180719174820181-1928988154.png）

##### 1. 本地搭建环境
* git init   
* git config user.name"你的用户名"
* git config user.email"注册github时使用的邮箱"
* git config --global user.name"你的用户名"(全局设置,可选)
* git config --global user.email"注册github时使用的邮箱" (全局设置,可选)
* ssh-keygen --global -t rsa -C "注册github时使用的邮箱"

##### 2. 将在.ssh/下生成的id_rsa.pub 内容复制到github上,关联远程仓库
* git remote add origin git@github.com:用户名/仓库名.git

##### 3. 在本地使用git
* 配置系列:
    1. 添加关联: git remote add origin git@配置的Host(默认为github.com):仓库地址
    2. 删除关联: git remote remove 关联分支
    3. 查看关联: git remote -v 
    
* 提交文件系列:
    1. 添加文件: git add 文件名
    2. 提交至本地仓库: git commit -m'*****'
    3. 提交至关联仓库: git push 本地分支 远程分支
    4. clone到本地: git clone 仓库地址
    5. fetch到本地: git fetch
    6. 查看状态: git status
    7. 查看日志: git log
    8. 更新指定版本: git fetch 配合 git reset 版本号 实现更新指定版本号到本地  
    9. 回溯版本: git log 配合 git branch 分支名 版本号 实现回退到指定版本号并放置到新的分支上  

* Git工作流程  
	1. 克隆本地库：从远程库上克隆完整的Git仓库（包括代码和版本信息）到本地； 
	2. 在本地库上修改代码：在本地库上根据不同的开发目的，创建分支，修改代码；  
	3. 提交到分支：在本地分支上提交代码；  
	4. 把修改合并到本地主分支：在本地库上提交更新，也就是说，把修改合并到本地主分支；  
	5. 远程库合并到本地主分支：把远程库上的最新代码fetch下来，跟本地主分支合并，如果存在冲突，那么解决冲突。  
	6. 把本地主分支提交到远程库：生成补丁（patch），把补丁发送给远程库。  

##### 4.在本地使用ssh配置多个关联账号
_若需要在同一台电脑上关联不同账号的git账号_,则需要通过ssh-agent bash 进行配置  
1. 设置配置文件, 一般选择在~/.ssh/下配置config文件.  
2. 文件内容格式如下:  
    ```shell script
    #备注
    # 用户1
    #别名，随便定 后面配置地址有用
    host Authorcai  
        #要连接的服务器 
        Hostname github.com
        #用户名
        User Authorcai
        #密钥文件的地址，注意是私钥
        IdentityFile ~/.ssh/id_rsa 
    
    # 用户2
    host ZWtu19
        Hostname github.com
        User ZWtu19
        IdentityFile ~/.ssh/id_rsa_**
    ```  
3. 设置配置文件后通过ssh添加密钥  
    ```shell script
        ssh-agent bash
        // 用户1 密钥
        ssh-add ~/.ssh/id_rsa
        // 用户2 密钥
        ssh-add ~/.ssh/id_rsa_**
        // 查看是否成功
        ssh-add -l
        // 测试能否连接
        ssh -T git@Host名.com
    ```
4. 在本地文件目录下需要:  
```shell script
# 初始化数据库
git init 
# 指定用户名和邮箱
git config user.name '用户名'
git config user.email '用户邮箱'
# 关联远程地址
git remote add origin git@(Host名):仓库地址
git 文件操作
```

##### 5.出现无法连接github导致push、clone等操作无法完成的情况

1. 检查网络连接  
2. 检查ssh服务是否开启  
3. 检查22端口是否打开  
4. 检查hosts代理是否可行  

本人在使用git push时出现了push失败的情况，检查后发现ping github.com 显示连接不上，推断是hosts代理的问题，遂去网上查询了github官网的若干ip地址  
（百度 域名ip查询即可），在找到可ping通的ip后，将'ip地址  github.com'加到/private/etc/hosts 的最后；
修改hosts后即可ping通，也可以完成上传下载的功能了。

