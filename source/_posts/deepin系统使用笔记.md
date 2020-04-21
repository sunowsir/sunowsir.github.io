---
title: deepin系统使用笔记
date: 2019-09-02 16:39:06
cover: title.jpg
tags: note
---

> 1. 如果你是小白用户并且没有人在旁边指导，那么建议不要自行更改本文给出的命令。
> 2. 图形界面相关的东西自行探索。



##  deepin系统安装后推荐配置
`sudo apt-get install -y git wget curl openssh-server manpages-* graphviz`


##  zsh配置（linux高级用户推荐）
  1. 安装：`sudo apt-get install zsh`
    
  2. 设置为默认SHELL(不要加sudo)：`chsh -s /bin/zsh`
  3. 安装oh-my-zsh
```bash
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

  4. 手动配置oh-my-zsh
       1. 安装自动跳转插件：
           1.` sudo apt-get install autojump`
           	2. 打开~/.zshrc，在文件末尾，另起一行添加：`source   /usr/share/autojump/autojump.sh`
           2. 安装zsh-syntax-highlighting语法高亮插件：
             1. `cd ~/ && git clone https://github.com/zsh-users/zsh-syntax-highlighting.git`
             2. `cd ~/ &&echo "source ${(q-)PWD}/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc`
           3. 安装zsh-autosuggestions语法历史记录插件:
             1. `git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions`
             2. 打开~/.zshrc，在文件末尾，另起一行添加：`source $ZSH_CUSTOM/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh`
        2. 打开~/.zshrc:
            1. 找到：plugins=(git)这个位置，在括号里面添加，每个单词单独一行，如果已经有了，就不用添加了：
                ```shell
                	git
                	extract
                	z
                	web-search
                	zsh-autosuggestions
                	cp
                	command-not-found
                ```

                2. 在文件末尾，另起一行添加：
                ```shell
                export EDITOR=vim
                setopt HIST_IGNORE_DUPS
                setopt no_nomatch
                ```
  5. 自动配置oh-my-zsh

```shell

         #!/bin/bash
         
         
         if [[ ${?} -eq 1 ]];
         then
             exit 1;
         fi
         
         
         sudo apt-get install autojump
         git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
         git clone git://github.com/zsh-users/zsh-autosuggestions  ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions
         
         
         echo '
         
         
         
         #########################################
         
         alias ls="ls --color=auto"
         alias dir="dir --color=auto"
         alias la="ls -a --color=auto"
         alias ll="ls -al --color=auto"
         alias vdir="vdir --color=auto"
         
         alias grep="grep --color=auto"
         alias egrep="egrep --color=auto"
         alias fgrep="fgrep --color=auto"
         
         alias cls="clear"
         
         export EDITOR=vim
         setopt no_nomatch
         setopt HIST_IGNORE_DUPS
         
         source /usr/share/autojump/autojump.sh
         source ~/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
         
         ' >>  ~/.zshrc
         
         
         sed -i 's/^plugins=(git)/plugin=\(extract \n  z \n web-search \n  zsh-autosuggestions \n cp \n command-no-found\)/g' ~/.zshrc
         
         
         
```

6. 通过手动或自动配置，zsh就彻底配置完成。

   ​     
## 常见文件
- 搜狗输入法皮肤所在路径：~/.config/sogou-qimpanel/skin
- desktop软件图标路径集合：
  - ~/.local/share/applications : AppImage应用生成的图标。
  - /usr/share/applications/ :  常用应用图标所在。
  - /etc/xdg/autostart/ : 系统级别自启动应用图标。
  - /opt/deepinwine/apps/ : deepin-wine应用图标。
  - /var/lib/flatpak/app/ : flatpak应用图标。
    以上所给路径仅为常见路径，并非所有。
- 
- 
## 常用命令（linux入门用户推荐）：
  - ls : 列出当前路径文件。

  - pwd : 查看当前所在路径（绝对路径）。
  - cd : 路径跳转。

  - mv : 文件及目录移动以及更改名字。
  - cp : 拷贝。
  - mkdir : 创建目录。
  - touch : 创建空白文件。
- 桌面设置壁纸的内置壁纸保存位置：
  如图：

  这些壁纸保存在：/usr/share/wallpapers/deepin下。
- vim 配置文件：~/.vimrc（用户级别配置文件，只针文件所在用户生效，其他用户不生效）
- bash配置文件：~/.bashrc（用户级别配置文件，只针文件所在用户生效，其他用户不生效）



##  vim 入门操作
  *  vim配置:
     1. vim的配置我们选择ma6174的配置，
         终端命令：wget -qO- https://raw.github.com/ma6174/vim/master/setup.sh | sh -x
         配置完成后会重新回到终端命令行（建议在网络较好的环境下配置）
     2. 配置完成后打开python文件会发现报错，解决方案：
        点击这里下载python.zip文件，将压缩包下载到本地解压，得到一个名称为python的文件夹，将其复制（覆盖并替换）到～/.vim/ftplugin/路径下即可。
  *  三种模式：
     - 	插入模式：
    1. 普通模式下按i直接进入插入模式。
    2. 普通模式下按I光标前一个位置进入插入模式。
    3. 普通模式下按O光标的下一行进入插入模式。
    4. 普通模式下按o光标的上一行进入插入模式。
  - 普通模式：
    - 在任何模式下按ESC进入普通模式。
    - 在普通模式下：
      - dd : 剪切当前行（可以当删除用）（只在普通模式和选择模式生效）。
      - yy：复制当前行（只在普通模式和选择模式生效）。
      - p ： 粘贴（只在普通模式生效）。
  - 选择模式：
    - c : 进入块选择模式。
    - C:  进入行选择模式。
    - CTRL + c : 进入列选择模式。
