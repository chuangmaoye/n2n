## windows
    1.先安装n2nguien.exe
    2.然后更改配置文件n2ngui.ini，修改里面的服务器地址supernode_IP = 服务器ip 和本地虚拟ip地址edge_IP = 1.2.3.10 注：1.2.3.2~1.2.3.254 都可用（47、48已经被占用）
    3.修改完之后把文件替换到n2nguien.exe的安装目录
    4.启动桌面上的n2n Gui程序（使用管理员权限运行） 点击ok 稍等片刻ping一下1.2.3.47
## linux
    1.进入n2n_v1目录，进行 make && make install 即可安装
    2.配置本地节点链接服务器
        nohup edge -d n2n0 -c myn2n -M 1200 -k liliangliang -a 1.2.3.2～254 -l 服务器ip:33333 -m 41:04:05:14:11:01 > /tmp/edge.log 2<&1 &
        参数说明 
            -a 后面是本机虚拟ip地址 1.2.3.2~1.2.3.254 范围
            -l 后面跟服务器地址和端口号
            -m 后面跟虚拟mac地址，按照mac规则随意修改即可
## mac
    待尝试
    brew install openssl
    brew install cmake
    编辑n2n_v2/CMakeLists.txt 文件, 找到set(CMAKE_C_FLAGS 和set(CMAKE_CXX_FLAGS 两行
    在这两行的里面括号里面的部分, 加入编译参数-I/usr/local/opt/openssl/include -L/usr/local/opt/openssl/lib
    在 n2n_v2 创建 build 文件夹, cmake .. 来创建Makefile, 然后make
    sudo make install即可安装
    sudo chmod -R 777 /usr/local/sbin
    ps 补充有些机器上可能会报错，通过加入参数-vf发现日志ERROR: Unable to open tap device，可以通过下面方式安装虚拟网卡:
    brew cask install tuntap
    查看是否有如下两个内核扩展
    ls /Library/Extensions/tap.kext
    ls /Library/Extensions/tun.kext
    校验内核扩展的参数
    find /Library/Extensions/{tap,tun}.kext/ -type f | xargs shasum
    加载内核扩展
    sudo /sbin/kextload /Library/Extensions/tap.kext
    sudo /sbin/kextload /Library/Extensions/tun.kext
    在尝试运行下连接试试应该就可以了,如果还是不行的话别忘记里尝试加上sudo用root权限执行下试试呢
