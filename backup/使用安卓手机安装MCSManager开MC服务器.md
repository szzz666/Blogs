#### 安装ubuntu
```
pkg install proot git python -y

git clone https://github.com/sqlsec/termux-install-linux
cd termux-install-linux
python termux-linux-install.py
```
####  启用ubuntu
```
cd ~/Termux-Linux/Ubuntu
./start-ubuntu.sh
```

> #### 配置自动启用ubuntu
> 在.bashrc文件中加上一行`bash ./Termux-Linux/Ubuntu/start-ubuntu.sh`
> 该.bashrc文件路径`/data/data/com.termux/files/home/.bashrc`

#### 更新清华源
在`/data/data/com.termux/files/home/Termux-Linux/Ubuntu/ubuntu-fs/etc/apt/sources.list`
文件里面添加一行：
`deb https://mirrors.tuna.tsinghua.edu.cn/termux/termux-packages-24 stable main`

#### 安装前置(xz gnupg git java vim)
```
apt gpg curl ca-certificates gnupg vim unzip
```
#### 更新libc6(node需要更高的版本)
在`/data/data/com.termux/files/home/Termux-Linux/Ubuntu/ubuntu-fs/etc/apt/sources.list`
文件里面添加一行：
`deb http://mirrors.ustc.edu.cn/debian-security buster/updates main`
信任秘钥
```
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 112695A0E562B32A 54404762BBB6E853
```
要保持网络稳定，直到出现下面两行代码，若未出现则重新进行上一步
```
gpg: Total number processed: 2          
gpg:               imported: 2
```
更新libc6
```
apt update
apt install libc6
```
#### 安装node
创建并移动到node文件夹
```
mkdir /usr/local/node
cd /usr/local/node
```
下载node的压缩包(ARM64/ARMV8)
```
wget https://nodejs.org/dist/v20.11.0/node-v20.11.0-linux-arm64.tar.xz
```
解压
```
#把.tar.xz文件解压为.tar文件
xz -d ./node-v20.11.0-linux-arm64.tar.xz
#解压.tar文件
tar -xvf ./node-v20.11.0-linux-arm64.tar
#删除文件
rm -r ./node-v20.11.0-linux-arm64.tar*
```
配置环境变量
```
sed -i '1 i NODE_HOME=/usr/local/node/node-v20.11.0-linux-arm64\nPATH=\$NODE_HOME/bin:\$PATH\nexport NODE_HOME PATH\n' /etc/profile
```
使配置生效
```
source /etc/profile
```
> 使用下面两条命令测试node，结果与井号内容类似即可
> ```
> node -v 
> #v20.11.0
> npm -v
> #10.2.4
> ```
#### 安装MCSManager
```
# 切换到安装目录，你也可以换成其他的目录。
cd /opt/

# 进入你的安装目录
mkdir /opt/mcsmanager/
cd /opt/mcsmanager/

# 下载 MCSManager（如果无法下载可以先科学上网下载再上传到服务器）
wget https://github.com/MCSManager/MCSManager/releases/latest/download/mcsmanager_linux_release.tar.gz

# 解压到安装目录
tar -zxf mcsmanager_linux_release.tar.gz
```
#### 启动MCSManager
安装screen
```
apt install screen
```
启动MCSManager
```
# 进入 /opt/mcsmanager 目录
cd /opt/mcsmanager

# 创建并进入一个新的 screen 会话
screen -dmS mcsmanager

# 在 screen 会话中运行 start-web.sh
screen -S mcsmanager -X screen -t web bash -c './start-web.sh; read'

# 在 screen 会话中运行 start-daemon.sh
screen -S mcsmanager -X screen -t daemon bash -c './start-daemon.sh; read'
```





