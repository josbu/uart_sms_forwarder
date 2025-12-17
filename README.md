# Air780E 短信UART转发器

基于 Air780E 设备的短信转发系统，支持接收短信并通过串口转发到上位机。

**已测试设备**

- Air780E
- Air780EHV


## 🌟 功能特性

- 📱 自动接收短信并转发到串口
- 🔄 支持双向通信（可通过串口发送短信）
- 📊 JSON格式数据传输
- 💾 消息缓存机制
- 🐕 看门狗保护
- 💓 心跳状态上报
- 🛡️ 错误处理和内存管理

## 截图

![screenshot1.png](screenshots/screenshot1.png)
![screenshot2.png](screenshots/screenshot2.png)

## 🚀 快速开始

### 1. 硬件准备

**Air780E 设备准备**：
- 插入有效的SIM卡
- 通过USB连接电脑

### 2. 烧录 Lua 脚本

使用 **LuaTools** 烧录 `main.lua` 脚本，第一次烧录需要点击 「下载底层和脚本」

![write.png](screenshots/write.png)

### 3. 测试

![test.png](screenshots/test.png)

### 4. 把设备插入到你的小主机等 Linux USB上


### 5. 运行上位机程序

下载

```shell
wget https://github.com/dushixiang/uart_sms_forwarder/releases/latest/download/uart_sms_forwarder-linux-amd64.tar.gz
```

解压
```bash
tar -zxvf uart_sms_forwarder-linux-amd64.tar.gz -C /opt/
mv /opt/uart_sms_forwarder-linux-amd64 /opt/uart_sms_forwarder
```

创建系统服务

```shell
cat <<EOF > /etc/systemd/system/uart_sms_forwarder.service
[Unit]
Description=uart_sms_forwarder service
After=network.target

[Service]
User=root
WorkingDirectory=/opt/uart_sms_forwarder
ExecStart=/opt/uart_sms_forwarder/uart_sms_forwarder
TimeoutSec=0
RestartSec=10
Restart=always
LimitNOFILE=1048576

[Install]
WantedBy=multi-user.target
EOF
```

启动服务

```shell
systemctl daemon-reload
systemctl enable uart_sms_forwarder
systemctl start uart_sms_forwarder
```

打开浏览器访问 8080 端口。

修改密码等配置项，请参考 [config.example.yaml](config.example.yaml) 文件。