## 配置Git

全局设置储存在 ~/.gitconfig 文件中，而本地设置储存在正在工作的仓库中的 .git/config 文件中。



### 查看当前设置

显示一个设置的值

```shell
git config --get user.name 
```

显示当前设置过的所有值的列表

```shell
git config --list
```



### 配置个人身份

1. 全局设置

   这里设置的`姓名`和`邮箱地址`会用在 Git 的提交日志中，会随着提交日志一同被公开。

   + 配置你的名字

    ```shell
    git config --global user.name 'Your Name' 
    ```

   + 配置你的电子邮件地址

    ```shell
    git config --global user.email 'Your email'
    ```

2. 特殊项目配置

   (1) 前往想要配置的仓库根目录。

   (2) 用 --local 替换 --global，然后应用配置命令。

   ```shell
   git config --local user.email 'Your email'
   ```



### 添加颜色提高命令输出的可读性

```shell
git config --global color.ui true 
git config --global diff.ui auto
```



### 更改提交说明编辑器

如果要使用 Vim，请使用以下命令

```
git config --global core.editor vim
```

如果想要更改 Windows 的编辑器，则需要加入应用文件的完整路径。

```
git config --global core.editor '"C:\Program Files\Vim\gvim.exe" --nofork'
```



### 忽略系统文件

1. 全局设置

   设置一个全局忽略文件让 Git 避免将临时提交到任何创建的本地仓库。

   在https://github.com/github/gitignore挑选最适合的系统和项目的列表。

   + 创建一个新的文本文件，名为 .gitignore_global，将它放在你的 home 目录下。 

   ```
   git config --global core.excludesfile ~/.gitignore_global 
   ```

     

2. 特殊项目设置

    在每个仓库中，都可以创建一个自定义的“忽略”文件，进一步限制 Git 要跟踪的文件。 

    + 创建一个新的文本文件，名为 .gitignore，将它放在你的项目根目录下。

    + 在这个文件中添加所有你希望 Git 永远不要添加到仓库的文件名称，每个文件名应该单独一行。

    ```shell
    git add .gitignore
    git commit -m "Adding list of files to be ignored."
    ```



### 行结束符问题

如果开发者分别使用 OS X、Linux 和 Windows，应该在全局设置这个行结束符，同时在每个仓库中添加这个设置。

```shell
git config --global core.autocrlf input 
```

需要在你的仓库中添加一个.gitattributes 文件，标记正确的行结束符、应该被改正的文本文件和不应该被修改的二进制文件。 在仓库根目录（与 .git 位于同一文件夹中）下创建一个名为 .gitattributes 的新文本文件。

```sh
# 设置所有文件的默认行为
*.text=auto

# 列出应使用系统相关的行结束符的文本文件
*.php text
*.html text
*.css text  

# 列出应使用CRLF行结束符且不根据本地操作系统转换的文件 
*.sln text eol=crlf  

# 列出所有不应进行修改的二进制文件 
*.png binary  
*.jpg binary  
*.gif binary  
*.ico binary 
```

```shell
git add .gitattributes
git commit -m "Require the right line endings for everyone, forever."
```



### 解决windows中文乱码

```shell
git config --global core.quotepath false
```

