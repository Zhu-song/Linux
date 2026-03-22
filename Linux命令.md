# 一、基础操作（入门必备，终端交互）
open -a app名称：打开app

| 命令       | 功能说明             | 实用实例                                                          |
| -------- | ---------------- | ------------------------------------------------------------- |
| ls       | 列出目录内容（文件 / 文件夹） | `ls -l`（详细列表）、`ls -a`（显示隐藏文件）、`ls /root`（列出指定目录）              |
| cd       | 切换目录             | `cd /root`（进入根目录下的 root 文件夹）、`cd ..`（返回上一级）、`cd ~`（回到当前用户家目录） |
| pwd      | 显示当前所在目录路径       | `pwd`（输出如 `/root/linux_amd64_server`）                         |
| clear    | 清空终端屏幕           | `clear`（快捷键 `Ctrl+L` 效果一致）                                    |
| exit     | 退出当前终端 / SSH 连接  | `exit`（断开 SSH 连接时使用）                                          |
| whoami   | 查看当前登录用户名        | `whoami`（输出如 `root`）                                          |
| hostname | 查看服务器主机名         | `hostname`（输出如 `nps-server`）                                  |
#  二、文件管理（创建 / 编辑 / 删除 / 查找，最常用）

| touch     |        创建空文件         | `touch nps.conf`（创建 NPS 配置文件）                                                                |
| --------- | :------------------: | -------------------------------------------------------------------------------------------- |
| mkdir     |        创建文件夹         | `mkdir /root/nps-logs`（创建 NPS 日志目录）、`mkdir -p a/b/c`（递归创建多级目录）                               |
| rm        |   删除文件 / 文件夹（谨慎使用）   | `rm test.txt`（删除文件）、`rm -rf nps-old`（强制删除文件夹及内容，`-rf` 不可恢复）                                  |
| cp        |      复制文件 / 文件夹      | `cp nps.conf nps.conf.bak`（备份配置文件）、`cp -r /root/nps /home/`（复制文件夹）                           |
| mv        |   移动 / 重命名文件 / 文件夹   | `mv nps.conf /etc/`（移动文件到 /etc 目录）、`mv old.txt new.txt`（重命名）                                 |
| cat       |    查看文件内容（适合小文件）     | `cat /etc/os-release`（查看系统版本）、`cat nps.conf`（查看 NPS 配置）                                      |
| find      | 查找文件 / 文件夹（按路径 / 名称） | `find / -name "nps"`（全系统查找 nps 相关文件）、`find /root -type f -name "*.log"`（查找 root 目录下的 log 文件） |
| grep      |    搜索文件内容 / 命令输出     | `grep "error" nps.log`（查找日志中的错误信息）、`ps -ef                                                   |
| head/tail |    查看文件开头 / 结尾内容     | `ead -10 nps.log`（查看前 10 行）、`tail -f nps.log`（实时查看日志更新，NPS 排错用）                              |
# 三、系统管理（服务器状态 / 配置，NPS 场景常用）

| uname       | 查看系统内核信息               | `uname -r`（查看内核版本，如 `3.10.0-1160.el7.x86_64`）、`uname -a`（完整内核信息）        |
| ----------- | ---------------------- | ----------------------------------------------------------------------- |
| hostnamectl | 查看系统详细信息（版本 / 内核 / 架构） | `hostnamectl`（一键查看操作系统、内核、架构等）                                          |
| df          | 查看磁盘空间使用情况             | `df -h`（以人类可读格式显示，如 `G/M`）                                              |
| du          | 查看文件 / 文件夹大小           | `du -sh /root/nps`（查看 NPS 目录总大小）                                        |
| top         | 实时查看系统资源占用（CPU / 内存）   | `top`（默认排序，`P` 按 CPU 排序，`M` 按内存排序，`q`退出）                                |
| uptime      | 查看服务器运行时间 / 负载         | `uptime`（输出如 `10:00:00 up 7 days, 2 hours, 3 users`）                    |
| timedatectl | 查看 / 设置系统时间            | `timedatectl`（查看时间时区）、`timedatectl set-timezone Asia/Shanghai`（设置时区为上海） |
| free        | 查看内存使用情况               | `free -h`（显示总内存、已用、空闲，如 `16G` 内存）                                       |
| reboot      | 重启服务器                  | `sudo reboot`（需 root/sudo 权限）                                           |
| shutdown    | 关闭服务器                  | `sudo shutdown -P now`（立即关机断电）、`sudo shutdown -h 10`（10 分钟后关机）          |
# 四、网络操作（SSH/NPS 连接 / 端口，核心场景）

| ip           | 查看 / 配置网卡 IP 信息          | `ip addr`（查看所有网卡 IP，如 `eth0` 的公网 / 内网 IP）、`ip route`（查看路由表）                                                              |
| ------------ | ------------------------ | ------------------------------------------------------------------------------------------------------------------------ |
| ping         | 测试网络连通性                  | `ping 123.45.67.89`（测试云服务器连通性）、`ping 192.168.3.188`（测试内网设备连通性，NPS 排错用）                                                   |
| netstat      | 查看端口占用 / 网络连接（CentOS）    | `netstat -tuln`（查看所有监听端口）、`netstat -tuln                                                                                 |
| curl         | 测试 HTTP 连接 / 下载文件        | `curl http://127.0.0.1:8080`（测试 NPS 管理面板是否可访问）、`curl -O https://xxx.com/nps.tar.gz`（下载 NPS 安装包）                          |
| firewall-cmd | 配置 firewalld 防火墙（CentOS） | `sudo firewall-cmd --add-port=8024/tcp --permanent`（开放 NPS 客户端通信端口）、`sudo firewall-cmd --reload`（重载防火墙）                  |
| ufw          | 配置 ufw 防火墙（Ubuntu）       | `sudo ufw allow 2222/tcp`（开放 SSH 自定义端口）、`sudo ufw status`（查看防火墙状态）                                                       |
| ssh          | 远程登录服务器                  | `ssh root@123.45.67.89 -p 2222`（用 2222 端口登录云服务器）                                                                         |
| scp          | 远程传输文件（本地↔服务器）           | `scp -P 2222 nps.tar.gz root@123.45.67.89:/root/`（本地传文件到服务器）、`scp -P 2222 root@123.45.67.89:/root/nps.log ~/`（服务器传文件到本地） |
# 五、权限管理（文件 / 文件夹权限控制，安全必备）

| sudo  | 临时获取 root 权限执行命令 | `sudo systemctl restart sshd`（用 root 权限重启 SSH 服务）                                                                            |
| ----- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| ls -l | 查看文件权限详情         | `ls -l nps`（输出如 `-rwxr-xr-x`，第一个 `-` 是文件，`rwx` 分别是读 / 写 / 执行权限）                                                              |
| chmod | 修改文件 / 文件夹权限     | `chmod +x nps`（给 NPS 可执行文件添加运行权限）、`chmod 700 ~/.ssh`（限制 SSH 密钥目录仅自己访问）、`chmod 600 ~/.ssh/authorized_keys`（SSH 密钥文件权限，必须 600） |
| chown | 修改文件 / 文件夹所有者    | `sudo chown root:root nps`（设置 nps 文件所有者为 root）、`sudo chown -R root:/root/nps`（递归修改文件夹所有者）                                    |
| chgrp | 修改文件 / 文件夹所属组    | `sudo chgrp root nps.conf`（设置配置文件所属组为 root）                                                                                  |
# 六、进程管理（启动 / 停止 / 查看进程）

| ps        | 查看进程状态               | `ps -ef`（查看所有进程）、`ps -ef                                                                                                                                                 |
| --------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| kill      | 终止进程（按进程 ID）         | `kill -9 1234`（强制终止 PID 为 1234 的进程，如 NPS 异常进程）                                                                                                                           |
| pkill     | 按进程名终止进程             | `pkill nps`（终止所有 nps 相关进程）、`pkill sshd`（终止 SSH 进程，谨慎使用）                                                                                                                  |
| systemctl | 管理系统服务（启动 / 停止 / 自启） | `sudo systemctl start nps`（启动 NPS 服务，需配置系统服务）、`sudo systemctl restart sshd`（重启 SSH 服务）、`sudo systemctl enable nps`（设置 NPS 开机自启）、`sudo systemctl status nps`（查看 NPS 服务状态） |
| nohup     | 后台运行进程（关闭终端不停止）      | `nohup ./nps start &`（后台启动 NPS 服务端，日志保存到 nohup.out）                                                                                                                      |
| screen    | 创建会话，后台运行进程（推荐）      | `screen -S nps-session`（创建 NPS 专属会话）、`./nps start`（在会话中启动 NPS）、`Ctrl+A+D`（退出会话，进程后台运行）、`screen -r nps-session`（重新进入会话）                                                   |
# 七、日志查看（服务器排错必备）

| tail       | 实时查看日志更新                | `tail -f /root/linux_amd64_server/logs/nps.log`（实时查看 NPS 运行日志，排错用）                                  |
| ---------- | ----------------------- | --------------------------------------------------------------------------------------------------- |
| grep       | 搜索日志中的关键字               | `grep "error" /root/nps.log`（查找 NPS 日志中的错误）、`grep "timeout" nps.log`（查找超时相关日志，适配之前的 i/o timeout 报错） |
| cat        | 查看完整日志（小日志）             | `cat /var/log/secure`（查看 SSH 登录日志，排查暴力破解）                                                           |
| journalctl | 查看系统服务日志（CentOS/Ubuntu） | `journalctl -u nps`（查看 NPS 服务的系统日志）、`journalctl -u sshd`（查看 SSH 服务日志）                               |
| less       | 分页查看大日志文件               | `less /var/log/messages`（系统全局日志，按 `q` 退出）                                                           |
# 八、软件安装 / 卸载（NPS / 依赖安装）

| yum  | CentOS 系统包管理器（安装 / 卸载）        | 安装：`sudo yum install -y openssh-server`（安装 SSH 服务）、`sudo yum install -y wget`（安装 wget 下载工具）；卸载：`sudo yum remove -y wget`                       |
| ---- | ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| dnf  | CentOS 8+/Fedora 包管理器（替代 yum） | `sudo dnf install -y screen`（安装 screen 工具）                                                                                                     |
| apt  | Ubuntu/Debian 系统包管理器          | 更新源：`sudo apt update`；安装：`sudo apt install -y openssh-server`、`sudo apt install -y net-tools`（安装 netstat 工具）；卸载：`sudo apt remove -y net-tools` |
| tar  | 解压 / 压缩文件（安装包处理）              | 解压：`tar -zxvf linux_amd64_server.tar.gz`（解压 NPS 安装包）；压缩：`tar -zcvf nps-backup.tar.gz /root/nps`（备份 NPS 目录）                                     |
| rpm  | CentOS 二进制包安装（.rpm 文件）        | `sudo rpm -ivh xxx.rpm`（安装 rpm 包）、`sudo rpm -e xxx`（卸载 rpm 包）                                                                                  |
| dpkg | Ubuntu 二进制包安装（.deb 文件）        | `sudo dpkg -i xxx.deb`（安装 deb 包）、`sudo dpkg -r xxx`（卸载 deb 包）                                                                                  |

**在虚拟机中查看公网IP：`curl icanhazip.com`。（原理：通过向第三方公网服务器发送HTTP请求，由服务器反向识别并返回你的出口公网IP，而非本地直接计算或获取。）**
**在macOS系统的iterm2中一般情况下，证书文件放在/Users/zhusong/.ssh下面。**
