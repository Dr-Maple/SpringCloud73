# Yakit-MuMu-App抓包-安卓调试桥
yakit抓小程序和App很行！！！
前期准备
1.下载MuMU模拟器
模拟器下载
2.安装adb
adb install
添加环境变量
3.安装openssl
openssl下载
MuMu模拟器操作
打开root权限及文件访问权限
下载证书
由于安卓7.0以上版本不再信任用户证书，所以我们需要给手机安装系统证书
看一下自己的IP 172.26.116.18
yakit添加代理监听
172.26.116.18 8888
证书下载
这里需要选择下载到本地，这时证书下载下来应该是pem格式
在证书的文件夹打开cmd终端
yakit的证书因为导出后就是pem格式可以省略第一步，直接查看证书哈希值
openssl x509 -inform PEM -subject_hash_old -in yakit证书.crt.pem
将文件名改为hash值最上方的数字，到这里证书就算制作成功
将yakit证书.crt.pem 改为 10fblfcc.0
导入系统证书
这里需要用到adb，不会adb的朋友可以去学习一下
adb devices
adb connect 127.0.0.1:16384
adb root 这时查看模拟器 可会有弹窗 点击永远允许
adb push 10fb1fcc.0 /system/etc/security/cacerts/
push的地址要正确 一定要将证书导入**/system/etc/security/cacerts/**
MuMu模拟器设置代理
与yakit代理监听ip相同
改为手动 设置ip 端口
查看yakit是否有数据包 成功！！！
