# zsh安装及配置

## 1. zsh 介绍

zsh 是一个兼容 bash 的 shell，相较 bash 具有以下优点：

- Tab 补全功能强大。命令、命令参数、文件路径均可以补全。
- 插件丰富。快速输入以前使用过的命令、快速跳转文件夹、显示系统负载这些都可以通过插件实现。
- 主题丰富。
- 可定制性高。

## 2. 安装 zsh

macOS：
`brew install zsh`

ubuntu：
`sudo apt-get install zsh`

ArchLinux/Manjaro：
`sudo pacman -S zsh`

>  - 安装好后，使用 `cat /etc/shells `查看系统可以用的 shell。
> - 使用 `chsh -s /bin/zsh `命令将 zsh 设置为系统默认 shell。(新开一个 Shell Session，就可以开始使用 zsh )

## 3. 安装 oh-my-zsh
使用 curl 下载脚本并安装：
`sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`

或者使用 wget 下载脚本并安装：
`sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"`

> 同意使用 Oh-my-zsh 的配置模板覆盖已有的 .zshrc
> 在配置过程中，脚本会提示将 zsh 设为默认的 shell

## 4. 配置 zsh

### 4.1 修改主题

在 [Themes](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes) 中查看内置的主题样式和对应的主题名。这些内置主题已经放在 `～/.oh-my-zsh/themes` 目录下，不需要再下载。

**powerlevel10k 主题安装**

`git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k`

使用 vim 编辑 .zshrc，键入以下内容并保存：
`ZSH_THEME="powerlevel10k/powerlevel10k" `

> 执行 source ~/.zshrc 配置生效，这时会提示对主题进行配置，按照提示进行即可。


### 4.2 安装插件
> 内置插件可以在 ～/.oh-my-zsh/plugins 中查看

#### zsh-autosuggestions

zsh-autosuggestions 是一个命令提示插件，当你输入命令时，会自动推测你可能需要输入的命令，按下右键可以快速采用建议。

安装步骤：

1. 把插件下载到本地的 `~/.oh-my-zsh/custom/plugins` 目录：
`git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions`

2. 在 .zshrc 中，把 zsh-autosuggestions 加入插件列表：

``` bash
plugins=(
    # other plugins...
    zsh-autosuggestions  # 插件之间使用空格隔开
)
```
3. 开启新的 Shell 或执行 `source ~/.zshrc`，就可以开始体验插件。

#### zsh-syntax-highlighting
> zsh-syntax-highlighting 是一个命令语法校验插件，在输入命令的过程中，若指令不合法，则指令显示为红色，若指令合法就会显示为绿色。

安装步骤：

1. 把插件下载到本地的 `~/.oh-my-zsh/custom/plugins` 目录:
`git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting `

2. 在 .zshrc 中，把 `zsh-syntax-highlighting` 加入插件列表：

``` bash
plugins=(
    # other plugins...
    zsh-autosuggestions
    zsh-syntax-highlighting
)
```

3.  开启新的 Shell 或执行 `source ~/.zshrc`，就可以开始体验插件了。

#### z
> z 是一个文件夹快捷跳转插件，对于曾经跳转过的目录，只需要输入最终目标文件夹名称，就可以快速跳转，避免再输入长串路径，提高切换文件夹的效率。

安装步骤：

1. 由于 oh-my-zsh 内置了 z 插件，所以只需要在 .zshrc 中，把 z 加入插件列表：
``` bash
plugins=(
     # other plugins...
     zsh-autosuggestions
     zsh-syntax-highlighting
     z
)
```

2. 开启新的 Shell 或执行 `source ~/.zshrc`，就可以开始体验插件了。

## windown 配置zsh
> 依赖于`git bash` ,需要安装
> 直接下载安装，或使用scoop（`scoop install git`）以scoop安装为例。
> 设置终端和vscode为Git-Bash

### 安装配置 git bash 

### 配置zsh

### zsh主题插件配置见上


## 参考
[Windows在git-bash安装zsh](https://blog.csdn.net/Layouwen/article/details/125924286)

[Windows下的Git Bash配置](http://ithb.vip/456.html)