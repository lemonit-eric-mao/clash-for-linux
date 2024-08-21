# 使用教程

## 下载项目

下载项目

```bash
$ git clone https://github.com/lemonit-eric-mao/clash-for-linux.git
```

进入到项目目录，编辑`.env`文件，修改变量`CLASH_URL`的值。

```bash
$ cd clash-for-linux
$ vim .env
```

> **注意：** `.env` 文件中的变量 `CLASH_SECRET` 为自定义 Clash Secret，值为空时，脚本将自动生成随机字符串。

---

## 启动程序
> `sudo bash start.sh`
```bash
$ sudo bash start.sh
CPU architecture: amd64

正在检测订阅地址...
Clash订阅地址可访问！                                      [  OK  ]

正在下载Clash配置文件...
配置文件config.yaml下载成功！                              [  OK  ]

判断订阅内容是否符合clash配置文件标准:
订阅内容符合clash标准

正在启动Clash服务...
服务启动成功！                                             [  OK  ]

Clash Dashboard 访问地址: http://<ip>:9090/ui
Secret: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

请执行以下命令加载环境变量: source /etc/profile.d/clash.sh

请执行以下命令开启系统代理: proxy_on

若要临时关闭系统代理，请执行: proxy_off

```

```bash
$ source /etc/profile.d/clash.sh

$ proxy_on
```

- 检查服务端口

```bash
$ ss -lntp | grep -E '9090|789.'
LISTEN 0      4096               *:7892            *:*    users:(("clash-linux-amd",pid=315944,fd=11))
LISTEN 0      4096               *:7890            *:*    users:(("clash-linux-amd",pid=315944,fd=8))
LISTEN 0      4096               *:7891            *:*    users:(("clash-linux-amd",pid=315944,fd=9))
LISTEN 0      4096               *:9090            *:*    users:(("clash-linux-amd",pid=315944,fd=7))

```

- 检查环境变量

```bash
$ env | grep -E 'http_proxy|https_proxy'
http_proxy=http://127.0.0.1:7890
https_proxy=http://127.0.0.1:7890
```

以上步鄹如果正常，说明服务clash程序启动成功，现在就可以体验高速下载github资源了。

---

## 重启程序

如果需要对Clash配置进行修改，请修改 `conf/config.yaml` 文件。然后运行 `restart.sh` 脚本进行重启。

> **注意：**
> 重启脚本 `restart.sh` 不会更新订阅信息。

---

## 停止程序

- 进入项目目录

```bash
$ cd clash-for-linux
```

- 关闭服务

```bash
$ sudo bash shutdown.sh

服务关闭成功，请执行以下命令关闭系统代理：proxy_off
```

```bash
$ proxy_off
```

然后检查程序端口、进程以及环境变量`http_proxy|https_proxy`，若都没则说明服务正常关闭。

---

## Clash Dashboard

- 访问 Clash Dashboard

通过浏览器访问`http://127.0.0.1:9090/ui`

- 登录管理界面
- ![image](https://github.com/user-attachments/assets/b139cd4c-94a3-45d3-bf26-565c63f2ee7b)

在`API Base URL`一栏中输入：`http://127.0.0.1:9090` ，在`Secret(optional)`一栏中输入启动成功后输出的Secret。

点击Add并选择刚刚输入的管理界面地址，之后便可在浏览器上进行一些配置。

- ![image](https://github.com/user-attachments/assets/7aee83f8-a017-43bc-82c8-380c1cc787bc)


