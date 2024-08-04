
# SSH配置多公钥

1. 生成SSH密钥对

```bash
ssh-keygen -t rsa -b 4096 -C nonll -f ~/.ssh/github/id_rsa_nonll
```
-t 这个选项后面跟的是密钥的类型
-b 这个选项后面跟的是密钥的位数。
-C 这个选项后面跟的是你想要添加到公钥中的注释信息
-f参数指定了密钥文件的存放位置和文件名。

2. 配置SSH客户端：
编辑或创建~.sshconfig文件，添加以下配置：

```bash
# GitHub
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/github/id_rsa_nonll
```
3. 复制公钥到GitHub：
复制生成的公钥内容到GitHub账户：

打开`~.sshgithubid_rsa_github.pub`文件，复制公钥内容。
登录GitHub，访问Settings  SSH and GPG keys。
点击New SSH key，将复制的公钥粘贴到相应的文本框中，并添加。


4. 测试SSH连接：
测试SSH连接到GitHub是否成功：

`ssh -T git@github.com`



成公钥后一步到位：

cat ~.sshid_ecdsa.pub  ssh root@192.168.48.100 mkdir -p ~.ssh && cat  ~.sshauthorized_keys  chmod 700 ~.ssh && chmod 600 ~.sshauthorized_keys


更改权限
chmod 600 ~.sshauthorized_keys
chmod 700 ~.ssh

打开公钥登录
编辑 

```bash
vi etcsshsshd_config  
# PubkeyAuthentication no改为yes
# wq! 强制保存并退出
```

查看 
```bash
cat etcsshsshd_config grep Pubkey
```

重启ssh服务

```bash
systemctl restart sshd.service
```
测试公钥登录
openssh登录
```bash
ssh -i 私钥位置 user@hostname
```

## 参考
[SSH配置公钥登录](httpswww.cnblogs.comxiondunp16810780.html)

[配置SSH服务器功能及参数](httpssupport.huawei.comenterprisezhdocEDOC1100262543379d8aea)

[SSH 多密钥配置](httpsblog.csdn.netyuhextarticledetails128767944)


[git配置多个ssh](httpsblog.csdn.netYC2chenarticledetails126973835)

[如何配置 SSH 管理多个 Git 仓库和以及多个 Github 账号](httpssegmentfault.coma1190000043924833)