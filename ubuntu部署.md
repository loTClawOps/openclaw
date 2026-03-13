# openclaw
# 一键开启ssh登录
	sudo apt update && sudo apt install -y openssh-server && sudo systemctl enable --now ssh
# gnome扩展增强(个人喜好改桌面配置)
	sudo apt install gnome-shell-extension-manager
	dash to Panel(charlesg99)
## 安装 OpenClaw（推荐）：
	curl -fsSL https://openclaw.ai/install.sh | bash
## 运行新用户引导向导：
	openclaw onboard --install-daemon
## 检查网关 
	openclaw gateway status
## 打开控制界面 
	openclaw dashboard
## 在前台运行网关，适用于快速测试或故障排除。 
	openclaw gateway --port 18789
## 3. 告诉网关重新加载配置
	openclaw gateway restart
## 重载配置：
	systemctl --user daemon-reload
## 重启网关：
	systemctl --user restart openclaw-gateway.service
## 检查状态：
	systemctl --user status openclaw-gateway.service
	journalctl --user -u openclaw-gateway.service -n 20
## (这个是给哪些要连接telegram等要代理的人使用，如果不用代理，可以忽略)安装 proxychains4
	sudo apt update && sudo apt install proxychains4 -y
## 配置代理：
	sudo nano /etc/proxychains4.conf
## 翻到最下面，把原来的 socks4 ... 删掉，改为你的代理（如果是 HTTP 代理）：
	dynamic_chain		// 删掉前面的 # 号,使其变亮 
	socks5 192.168.14.168 10808		//修改成你的代理地址
	localnet 127.0.0.0/255.0.0.0	// 删掉 localnet 前面的 # 号，使其变亮：
### 代理测试
	proxychains4 curl -I https://www.google.com		
### 第一步：停止当前运行的服务
### 由于它是被 systemd 托管的，简单的 pkill 可能会导致它自动重启。请使用以下命令彻底停止它：
	systemctl --user stop openclaw-gateway.service
### 第二步：使用代理手动启动
### 现在你可以使用 proxychains4 调用它的完整路径来启动了：
	proxychains4 /home/openclaw/.npm-global/bin/openclaw gateway run
注：如果系统依然提示找不到命令，请务必使用上面的完整路径。

### 永久让服务走代理
如果你希望以后每次开机自启都带代理，而不是每次手动运行，你可以修改它的服务配置文件：
### 编辑服务文件：
	nano ~/.config/systemd/user/openclaw-gateway.service
找到 ExecStart= 这一行，在命令前加上 proxychains4：
	ExecStart=/usr/bin/proxychains4 /usr/bin/node ... (后面的保持不变)
保存退出，执行 systemctl --user daemon-reload 然后重启服务。
### 使用 proxychains 强制启动
	proxychains4 openclaw gateway run
### 更新openclaw及更新后三部曲
	openclaw update					//更新到最新版
	openclaw doctor --fix			//清理缓存并重新对齐
	openclaw security audit --fix	//安全基准刷新
	openclaw --version				//验证版本
                                                             
