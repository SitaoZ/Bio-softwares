### DeepSeek 本地化部署

#### Windows 安装教程
- 第一步 安装 Ollama  本地部署前置工具

```bash
https://ollama.com/download
```
安装前切记关闭windows的防火墙，避免系统自动关闭下载

- 第二步 检查ollama安装是否成功  

打开CMD检查，Ollama是否正常安装成功，CMD进入，`ollama help` 正常返回帮助信息即可。
如果出现错误，第一：检查C盘是有有足够的空间，第二：检查防火墙是否关闭



- 第三步 下载DeepSeek-r1模型  

在ollama搜索deepseek-r1模型，选择合适的版本下载，和自己电脑的显存适配，
如果安装不成功，需要回去检查C盘的空间是否足够，因为默认安装在C盘。
```bash
ollama run deepseek-r1:14b
```

等模型下载完成，可以直接在命令行直接使用deepseek

- 第四步 搭建自己的知识库体系

`安装词嵌入模型`   

自家在搭建知识库时，需要加入的嵌入模型   
回到ollama网页界面，搜索`dmeta-embedding-zh`模型，点击进去，复制`ollama pull shaw/dmeta-embedding-zh`


- 第五步 安装Cherry studio AI知识库集成软件      
```bash
https://cherry-ai.com/
```

- 第六步 美化本地部署的deepseek-r1对话框   
使用Cherry studio AI来进行输入框美化，   
点击设置，选择`Ollama`，然后选择`deepseek-r1:14b`

- 第七步，搭建独属自己的AI知识库体系
点击`知识库`--`添加`   
名称自定义，嵌入模型选择自己下载词嵌入模型`shaw/dmeta-embedding-zh`，zh是中文模型的词向量。


- 第八步 对比正常的deepseek-r1和添加了知识库的模型   
点击`助手`，输入问题后选择指定的`知识库`
