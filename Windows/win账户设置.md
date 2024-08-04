## 1. 取消PIN登录
1. 点击设置->账户->登录选项
2. 点开“PIN”，选择“取消”， 如果“取消是虚字，不可选，则往下看， 找到”其他设置， 为了提高安全性，。。。",把这个开关选择“关”，再回到“PIN”， “取消”选择应该可以选. 然后会出现问题，如”你确信要取消.."之类， 选“确定”
3. 重新启动，发现不要PIN code 登录了， 但是需要password 登录.
> 此时，是使用微软账户登录

## 2. 微软账户更改本地账户登录
> Win11使用本地账户登录的方法

1. 首先点开底部“ windows徽标 ”，在上面找到并打开“ 设置 ”。
2. 然后进入左边栏的“ 账户 ”，打开右边的“ 账户信息 ”。
3. 打开后，在账户设置里选择“ 使用本地账户登录 ”。

## 3. 开机自动登录
1. 按“WIN+R”键打开“运行”输入 ms-settings:signinoptions 按确定打开“登录选项”，找到“为了改善安全性，仅在此装置上允许Microsoft 帐户的Windows Hello 登入”选项，把它设为关闭。
2. 按“WIN+R”键打开“运行”输入 “regedit”按 确定，打开注册表，找到「HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\PasswordLess\Device\DevicePasswordLessBuildVersion」，把右方的「DevicePasswordLessBuildVersion」值从2 改成0，
> 注意：修改保存后需重启电脑才生效。

3. 按“WIN+R”键打开“运行”输入 “netplwiz”按 确定，
4. 打开帐户设定“要使用本计算机，用户必须输入用户和密码”的选项取消打勾，按“确定”之后会弹出“自动登录”界面如图四，输入电脑用户与密码，确定就可以，以后开机默认就自动登录。


## 参考

[Windows 11: 登录电脑不需要用 pin code 或者密码password](https://blog.csdn.net/m0_60558800/article/details/123769129)
[Win11怎么改用本地账户登录？Win11使用本地账户登录的方法](https://www.xitongzhijia.net/xtjc/20230417/286680.html)
[Win10/Win11 设置开机自动登录的方法](https://zhuanlan.zhihu.com/p/624433183?utm_id=0)