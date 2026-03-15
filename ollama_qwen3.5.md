# ollama_qwen3.5
# 官网：https://ollama.com/
# 安装ollama
    irm https://ollama.com/install.ps1 | iex  //安装ollama，模型框架
    ollama run llama3.2  //安装小模型，在运行一次，即可运行模型
    
    ollama run qwen3.5:27b  //安装模型，
    ollama list (或 ollama ls)：列出所有已下载到本地的模型及其大小。
    ollama pull <模型名>：仅下载模型（如 qwen3.5:9b），不立即运行。
    ollama rm <模型名>：删除本地模型以释放硬盘空间。
    ollama show <模型名>：显示模型的详细信息，如配置文件、许可协议和参数。
    ollama cp <源模型> <新名字>：复制并重命名模型，常用于基于现有模型创建自定义版
    # 
