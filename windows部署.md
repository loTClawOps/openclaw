# Openclaw
以下所有命令在powershell里面执行（管理员身份运行）
"Windows detected — OpenClaw runs great on WSL2! Native Windows might be trickier."
### 准备工作：
# 1、解除脚本限制（仅需执行一次）：
		Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
# *安装git
		winget install --id Git.Git -e --source winget			//安装git
	关键一步：重启 PowerShell。关闭现在的窗口，重新开一个新的管理员权限的 PowerShell 窗口。如果不重启，系统可能还认不到刚装好的 git 命令
		git --version											//可以查看到版本，说明安装成功
# 2、建议执行，也可以忽略
		$PSVersionTable.PSVersion //查看powershell版本，建议PowerShell 7
		winget search --id Microsoft.PowerShell //搜索最新版本的 PowerShell
		winget install --id Microsoft.PowerShell --source winget  	//安装 PowerShell 7，安装完后用PowerShell 7管理员身份运行，在输入下面命令即可。
	
# 3、在线安装
		iwr -useb https://openclaw.ai/install.ps1 | iex		//就这一个命令搞定，在线安装
		openclaw doctor --fix								//一键修复命令，修复网关，配置文件
		openclaw tui 										//openclaw命令交互模式
		openclaw models list 								//模型列表
		openclaw gateway restart							//重启网关
		openclaw daemon stop								//停止网关
		openclaw daemon start								//启动网关
		penclaw gateway --force								// 最暴力的“强制重启”
		openclaw onboard									//交互式设置向导
		openclaw onboard --install-daemon					//如果你想连同后台常驻服务（Daemon）一起重新配置，可以使用
		openclaw onboard									//重新配置
		openclaw /skills install <名称>						//### 安装skill		
	
# 卸载：(如果安装过程或者配置过程有问题，卸载重新安装是最好的办法)
		openclaw gateway stop
		schtasks /delete /tn "OpenClaw Gateway" /f
		npm uninstall -g openclaw
		Remove-Item -Path "$HOME\.openclaw" -Recurse -Force
		[Environment]::SetEnvironmentVariable("OPENCLAW_TOKEN", $null, "User")
		[Environment]::SetEnvironmentVariable("ANTHROPIC_API_KEY", $null, "User")
安装结束后会自动出现提示信息，请根据提示信息完成 OpenClaw 配置，参考配置如下
# <img width="1577" height="457" alt="image" src="https://github.com/user-attachments/assets/3931fd7a-80de-42d8-b1ce-d7e237ec6b11" />

<img width="997" height="843" alt="image" src="https://github.com/user-attachments/assets/6e393730-ac0f-452d-a4af-7e7429121731" />

# minimax api key申请：https://minimaxi.com/

# <img width="997" height="843" alt="image" src="https://github.com/user-attachments/assets/98c8418e-5b2a-49b3-9fd7-509e309118c4" />

# <img width="997" height="583" alt="image" src="https://github.com/user-attachments/assets/2e170462-bd04-4156-88e3-1824ecd40ef0" />

# <img width="1920" height="911" alt="image" src="https://github.com/user-attachments/assets/a2261a33-3b19-45e2-885c-33528b05e3eb" />

# <img width="1920" height="1032" alt="image" src="https://github.com/user-attachments/assets/cfa49ecc-1940-403d-a244-005d10753ef3" />
# skill安装：
## 1. 文档与内容处理（你作为 IT 工程师可能最需要的）
### 📄 nano-pdf: 让 AI 能够读取和解析 PDF 文件。
### 🧾 summarize: 自动总结长文章、网页或文档的要点。
### 💎 obsidian: 如果你用 Obsidian 做笔记，这个技能让 AI 可以读取或写入你的笔记库。
### 🎙️ openai-whisper: 语音转文字。给它一段音频，它能吐出文字。

## 2. 开发与系统管理
### 🐙 github: 让 AI 可以操作你的 GitHub 仓库（提交代码、看 Issue 等）。
### 🧩 clawhub: OpenClaw 的插件中心，方便下载更多扩展。
### 🧿 oracle: 数据库连接工具（虽然叫 Oracle，但也常用于处理结构化数据查询）。
### 🎞️ video-frames: 视频帧提取。如果你需要 AI 分析视频里的某个画面，它能派上用场。

## 3. 日常办公与通讯
### 📧 himalaya: 一个命令行邮件客户端。安装后 AI 可以帮你读邮件、发邮件。
### 📱 wacli: WhatsApp 的命令行接口，让 AI 接入 WhatsApp。
### 🗣️ sag: 简单的语音合成，让 AI 能开口说话。
### 🔐 1password: 如果你用 1Password 管理密码，它能让 AI 安全地获取授权信息。

## 4. 媒体与娱乐
### 🌊 songsee / 🔊 sonoscli: 音乐搜索和 Sonos 音响控制。
### 🎮 gog: 关联 GOG 游戏平台。
### 🧲 gifgrep: 搜索并制作 GIF 动图。

## 5. 其他垂直工具
### 📰 blogwatcher: 监控博客更新。
### 📍 goplaces: 地点搜索和地理位置相关功能。
### 💡 openhue: 控制飞利浦 Hue 智能灯具。
### 🍌 nano-banana-pro: 通常是一个图像生成或高级图像处理的封装工具。

## 我的建议：
### 作为一个处理 SQL 数据库、OA 报表和代码开发的 IT 专业人士，建议你优先关注：
### nano-pdf 和 summarize（处理办公文档必选）。
### github（如果你要把代码传到你那个 KaspaLoT.com 的 GitHub Pages 上）。
### oracle（如果你后续想让 AI 直接读取你的 MySQL/SQL Server 数据）。
### 现在怎么选？
### 由于安装这些依赖可能还需要配置其他的 API Key（比如 GitHub 的 Token），我建议你先保持默认的 [•] Skip for now。

# 是否要开启 “钩子” (Hooks) 		//在自动化和开发领域，Hooks 就像是“自动触发器”，能在特定的时间点（比如 AI 启动时、对话结束时）自动执行一些预设的任务。
## 1. 选项具体解释
### 🚀 boot-md (启动说明书)
### 作用：每次启动 OpenClaw 时，它会自动读取并显示一个 Markdown 格式的说明文档。
### 需求度：低。如果你已经熟悉怎么用了，不需要每次启动都看一遍说明。

## 📎 bootstrap-extra-files (自动加载额外文件)
### 作用：启动时自动加载你指定的某些参考文件。比如你有一份 “SAP B1 数据库字典” 或者 “公司 OA 报表规范”，开启后可以让 AI 默认就“读过”这些背景资料。
### 需求度：中。如果你有固定的业务文档想让 AI 随时待命，这个很有用。

## 📝 command-logger (命令日志记录器)
### 作用：把你和 AI 的所有交互、AI 执行的每一个系统命令都记录在日志文件里。
### 需求度：高 (推荐)。作为系统管理员，保留操作审计日志（Audit Log）是一个好习惯，万一自动化脚本执行出了问题，可以翻日志找原因。

## 💾 session-memory (会话记忆)
### 作用：让 AI 记住你们之前的聊天上下文，避免“转头就忘”。
### 需求度：极高 (必选)。开启后，你上次聊到一半的 SQL 调试，下次进来还能接着聊。

# 完成！！！！
