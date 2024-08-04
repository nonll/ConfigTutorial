# 安装miniconda
## Windows
## Ubuntu
### 1. 安装准备工作
``` bash
sudo apt-get update 
sudo apt-get install build-essential
sudo apt-get install wget
```
其中，第一条命令表示更新包列表，第二条命令表示安装构建必需工具，第三条命令表示安装wget，用于从网络下载miniconda安装包。

### 2. 下载miniconda安装包
可以通过官方网站[下载](https://docs.conda.io/en/latest/miniconda.html)miniconda安装包，也可以使用wget从命令行中下载安装包。

``` wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh ```

下载完成后，使用以下命令给下载的安装包添加可执行权限：
``` chmod +x Miniconda3-latest-Linux-x86_64.sh ``` 

### 3. 安装miniconda
使用以下命令安装miniconda：

`./Miniconda3-latest-Linux-x86_64.sh`

安装过程中会出现一些提示，一般来说只需要按照提示按回车键即可。在安装过程中，需要同意许可协议并选择安装路径。如果不确定安装路径，可以选择默认路径。

### 4. 配置环境变量
安装完成后，需要配置miniconda的环境变量，这样才能在终端中使用conda命令。
首先，需要打开.bashrc文件：
`nano ~/.bashrc`
在文件末尾添加以下内容：
`export PATH="/home/username/miniconda/bin:$PATH"`
其中，username应替换为自己的用户名，安装路径也可能不同。
在保存文件并退出后，使用以下命令使配置生效：
`source ~/.bashrc`
现在，可以在终端中使用conda命令了。

### 5. 添加conda源
如果直接使用官方源下载软件包速度较慢，可以添加清华大学的源来加速下载。

打开终端，输入以下命令：

``` bash
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --set show_channel_urls yes
```
以上命令将清华大学的conda源添加到本地的配置文件中。之后，conda会优先从清华大学的源中下载软件包。

### 6. 建立新环境
可以通过conda命令来建立新环境。例如，以下命令将创建名为myenv的环境：

`conda create -n myenv`
创建完成后，需要激活环境。使用以下命令激活myenv环境：

`conda activate myenv`

### 7. 其它

1. 不自动激活base环境
 ```bash
 # 不自动激活base环境
 conda config --set auto_activate_base false
 # 自动激活base环境
 conda config --set auto_activate_base true
 ```
 2. 运行  `conda info` 命令，出现` base environment：...(onlyread)`。即无法创建新环境。
 
只需修改anaconda3文件夹权限，命令如下：
```bash
# 注意 username改为自己的用户名
sudo chown -R username anaconda3
sudo chown -R username .conda
```

3. .condarc文件

```bash
channels:
# 源
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - defaults
envs_dirs:
# 环境安装路径
  - /opt/miniconda3/envs
pkgs_dirs:
# 包，库下载路径
  - /opt/miniconda3/pkgs
show_channel_urls: true
# 不自动激活base环境
auto_activate_base: false
```