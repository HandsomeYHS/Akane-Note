# SVN ( Subversion)

跟踪文件的修改

### 客户端下载
下载地址1：https://tortoisesvn.net/downloads.html

下载地址2: https://sourceforge.net/projects/win32svn/

### 名词概念
- Checkout 检出，提取，创建工作副本
- Commit 提交
- Update 更新，同步
- Status 变动列表
- Revert 重置工作副本，撤销
- Merge 合并
- Resolve 帮助用户找出冲突并告诉版本库如何处理这些冲突
- trunk 主干线，主版本

---

### 基本命令

查看版本
```
svn --version
```

访问库
``` 
windows键+R, 访问库： svn://192.168.0.1/
```

创建版本库
```
svnadmin create 库名
```

svnserve启动服务
```
svnserve -d -r 目录 --listen-port 端口号
```
- **-r：** 配置方式决定了版本库访问方式。
- **--listen-port：** 指定SVN监听端口，不加此参数，SVN默认监听3690


svn检出操作
```
svn checkout url
```

查看版本库信息
```
svn info
```

查看版本作者，日期等
```
svn log
```

查看变更信息
```
svn diff
```

取得在特定版本的某文件显示在当前屏幕
```
svn cat
```

显示一个目录或某一版本存在的文件
```
svn list
```

查看工作副本状态
```
svn status
如果是?，说明未加入到版本控制中
```

添加到版本控制中
```
svn add .
svn add 文件名
```

提交
```
svn commit -m "描述提交信息"
```

更新
```
svn update
也可以指定版本，如下：
svn update 版本
```

版本回退-放弃文件修改
```
svn revert
svn revert -R trunk
注：trunk为所要放弃修改的文件或版本
```

合并版本
```
svn merge 分支目录
```

### 解决冲突

先更新，再提交，选择需要的东西






