# 基础操作
[CSDNgit常用命令](https://blog.csdn.net/qtiao/article/details/97783243#:~:text=Git%20%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4%E7%9A%84%E4%BD%BF%E7%94%A8%201%20git%20config%20%EF%BC%9A%E9%85%8D%E7%BD%AE%E4%BF%A1%E6%81%AF%202%20git,7%20git%20rm%20%EF%BC%9A%E5%88%A0%E9%99%A4%E5%91%BD%E4%BB%A4%208%20git%20mv%20%EF%BC%9A%E7%A7%BB%E5%8A%A8%E6%88%96%E9%87%8D%E5%91%BD%E5%90%8D%E5%91%BD%E4%BB%A4)
## 配置用户名 邮箱
``` git
git config --global user.name 用户名
git config --global user.email 邮箱
```
* 注:电子邮箱并不需要真实存在，尤其是在非正式情况下可以随便编写。
## 在github上下载源码
```git
git clone 地址
```
### 管理自己的文件夹
* 在一个文件夹下输入，表示初始化这个文件夹，让git进行管理。
* 获得一个.git文件夹，但是注意尽量不要直接操作这个文件夹。
```git
git init
```
### 上传文件
```git
git add .
```
* 命令git将当前目录下的所有文件和非空文件夹，设置为准备提交状态。
  >就是选中文件，准备对你选的文件进行操作。
  >. 是当前文件夹的意思。
### 注释
git commit 将缓存区内容添加到仓库中，可以在后面加-m选项，以在命令行中提供提交注释，格式如下：
```git
git commit -m "第一次版本提交"
```
如果你觉得 每次 commit之前要add一下，想跳过add这一步，可以直接使用 -a选项,如：
```git
git commit -am "第一次版本提交"
```
### 取消缓存区文件
git reset HEAD 命令用于取消已缓存的内容，如我们要取消已提交的test.txt文件
```git
git reset HEAD test.txt
```
### 查看提交的历史记录
```git
git log
```
## 恢复上一次提交
```git
git checkout HEAD 文件
```