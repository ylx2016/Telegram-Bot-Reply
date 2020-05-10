# Telegram Bot Reply

![GitHub release (latest by date)](https://img.shields.io/github/v/release/fhyuncai/Telegram-Bot-Reply?style=flat-square)
![GitHub](https://img.shields.io/github/license/fhyuncai/Telegram-Bot-Reply?style=flat-square)

> 通过 Telegram bot 通知和回复博客评论。

## 当前版本

Plugin：V1.1 (2020/05/10)

Proxy (PHP)：V1.01 (2020/04/26)

Proxy (Python)：V1.0 (2020/04/26)

## 作者

[FHYunCai](https://yuncaioo.com)

## 安装教程

前往 [Release 页面](https://github.com/fhyuncai/Telegram-Bot-Reply/releases/latest)下载源代码并将 tgbot-reply 文件夹解压到 WordPress 插件目录 (/wp-content/plugins/)，前往 WordPress 后台启用并配置相关信息。

如需使用回复功能，需在**保存配置后**点击 “更新 Telegram Bot Webhook” 按钮更新 Telegram bot webhook 配置。

## 使用方法

插件配置完成后，如果需要回复评论，只需回复 Bot 发送的消息即可。

如需删除新评论，回复需要删除的评论 “[Del]” 即可。

## 注意事项

### 代理服务

使用本插件需连接 Telegram 服务器，但在中国大陆的服务器无法直连 Telegram 服务器，为了方便使用故提供了代理服务程序。

#### PHP 版

将 proxy-tool-php 内的 proxy.php 以及 WordPress 本插件目录内的 SecertKey.php (需要启用插件才会生成) 上传至可直连 Telegram 的 Web 服务器 (PHP Version >= 5.3)，并在插件设置页面配置访问 proxy.php 的地址 (如：https://example.com/proxy.php) 即可。

#### Python 版

将 proxy-tool-python 内的所有文件上传至可直连 Telegram 的服务器，并执行以下命令安装所需模块：

```
pip3 install -r requirements.txt
```

安装完成后编辑 proxy.py 文件，修改第 13 行的 SecertKey 与 WordPress 本插件目录内 SecertKey.php 中的 SecertKey 一致，保存后执行以下命令启动服务：

```
python3 proxy.py
```

服务启动后在插件设置页面配置代理地址 (如：http://111.111.111.111:64321/proxy) 即可。

*注：如需后台运行服务可使用 screen, nohup, systemd 或 Supervisor 运行程序*

##### systemd 配置

```
# /usr/lib/systemd/system/proxy-tool-python.service

[Unit]
Description=Telegram Bot API Proxy
Documentation=https://github.com/fhyuncai/Telegram-Bot-Reply
After=network.target

[Service]
ExecStart=/usr/bin/python3 /path/to/proxy-tool-python/proxy.py
Restart=always

[Install]
WantedBy=multi-user.target
```

##### Supervisor 配置

```
[program:proxy-tool]
process_name=%(program_name)s
command=python3 /path/to/proxy-tool-python/proxy.py
autostart=true
autorestart=trueili.log
redirect_stderr=true
stdout_logfile=/var/log/proxy-tool-python/proxy-tool.log
```

## 更新日志

* 1.1 (2020/05/10)

    **注意！此版本需更新 Webhook！**

    修改 评论者若没有填写网址则返回 “无”

    新增 Webhook 首次使用及版本不一致提示

    新增 删除评论功能

* 1.0 (2020/04/25)

    Telegram Bot Reply 的第一个版本
