### Iterm2 环境搭建

1. 安装brew

   > /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

2. 安装iterm2

   >brew cask install iterm2

3. 安装oh-my-zsh

   > git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
   >
   > cd ~; mv ~/.zshrc ${HOME}/Library/Mobile\ Documents/com~apple~CloudDocs/Settings/zsh/zshrc
   >
   > ln -s "${HOME}/Library/Mobile Documents/com~apple~CloudDocs/Settings/zsh/zshrc" ~/.zshrc

4. 转换成zsh

   > chsh -s /bin/bash
   >
   > chsh -s /bin/zsh
   >
   > 查看当前的shell：ps -p $$

5. 下载solarized配色方案

   > git clone git://github.com/altercation/solarized.git

6. ssh 配置文件，直接关联iCloud

   ```
   cd ~; ln -s "/Users/feng/Library/Mobile Documents/com~apple~CloudDocs/Settings/ssh" .ssh
   cd ~/.ssh;find . -name "id_rsa"|xargs chmod 600
   ```

7. fzf [A command-line fuzzy finder](https://github.com/junegunn/fzf)

   > brew install fzf
   >
   > /usr/local/opt/fzf/install

8. autojump [A cd command that learns - easily navigate directories from the command line](https://github.com/wting/autojump)

   > brew install autojump
   >
   > j notes 会自动跳转到~/workspace/gitHub/notes目录

9. Awesome shell

   > 1. tree
   > 2. 