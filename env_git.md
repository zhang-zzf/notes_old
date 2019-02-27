1. 添加用户名和邮箱

   > git config --global user.name "zhanfeng.zhang"
   >
   > git config --global user.email "zhanfeng.zhang.ga@gmail.com"

2. 配置全局gitignore

   > [AutoGenerateSite](https://www.gitignore.io/) 生成内容cp到~/.gitigonre_global
   >
   > git config --global core.excludesfile "~/.gitignore_global"



## iCloud 软连接，可以在Mac系统之间共享

>cd ${HOME}/Library/Mobile\ Documents/com~apple~CloudDocs/Settings/Git
>
>mv ~/.gitconfig gitconfig
>
>mv ~/.gitignore_global gitignore_global
>
>ln -s ${HOME}/Library/Mobile\ Documents/com~apple~CloudDocs/Settings/Git/gitconfig ~/.gitconfig
>
>ln -s ${HOME}/Library/Mobile\ Documents/com~apple~CloudDocs/Settings/Git/gitignore_global ~/.gitignore_global

