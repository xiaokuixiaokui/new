基于ChatGLM人工智能模型应用与开发
一、项目概述
本项目旨在将ChatGLM（一个基于通用语言模型（GLM）的中文对话生成模型）与gec6818开发板相结合，实现一个可以在嵌入式设备上运行的智能对话系统。ChatGLM模型将用于处理用户输入的自然语言，生成相应的回复，并通过gec6818开发板进行实时交互。
本项目的扩展性很强因为ChatGLM 模型使用了来自互联网的大量文本数据进行训练，包括网页、书籍、新闻、文章、社交媒体帖子等等。这些数据包括了多种主题、多种语言和多种风格，模型拥有非常丰富的语言知识，学生可以根据自己的想法设计属于自己的物联网AI产品！
二、开发环境
1. 硬件设备
gec6818开发板：用于运行模型推理和与用户进行交互。
必要的硬件接口（如串口、USB等）：用于与PC或其他设备通信。
2. 软件环境
Linux操作系统（推荐）：用于在gec6818开发板上运行。
Ubuntu24.04环境：用于开发和部署SDK ChatGLM模型。
智谱AI开发平台(http://open.bigmodel.cn/)：用于加载开发和调试测试模型。
必要的库和工具：如SecureCRT、serial、Numpy等，用于数据处理和串口通信。
三、项目结构
├── 项目 # 项目文档，包括此README文件 
├── chatglm_stream.py # ChatGLM模型的加载和推理
├──  项目依赖库  requirements.txt
│    ├── Alsa库  #gec6818开发板音频录制播放
│    ├──讯飞语音识别库  #音频语音识别
│    ├── font.h and libfont.a  #freetype字库
│    ├──cjson/cJSON.h  #数据解析
│    ├── ekho.h  #文字转语音
│    └── sqlite3.h  #sqlite3数据库
├──iat_online_sampler.c  #服务器源代码
└──clien.c  #客户端源代码
四、开发步骤
1.环境搭建
在GEC6818开发板上搭建Linux操作系统环境。
配置交叉编译环境，确保能够在电脑上编译生成适用于GEC6818开发板的可执行文件。

安装依赖库 使用 pip 安装依赖： pip install -r requirements.txt，其中 transformers 库版本推荐为 4.27.1，但理论上不低于 4.23.1 即可。
从 Hugging Face Hub 下载模型需要先安装Git LFS，然后运行 git clone https://huggingface.co/THUDM/chatglm-6b  Hugging Face Hub 全球最大的开源AI模型社区。 
下载ChatGLM源码git clone https://github.com/THUDM/ChatGLM-6B 
cd ChatGLM-6B 
运行模型文件 python web_demo.py 运行网页版的代码 python cli_demo.py 运行本地版本的代码 python api.py 运行网页HTTP请求版本

2.加载ChatGLM模型
将ChatGLM模型文件转化为GEC6818开发板可加载的格式（如使用模型量化技术降低显存占用）。
将转化后的模型文件部署至GEC6818开发板的存储介质中。

sudo apt-get update #1.更新本地的软件列表
gec@DESKTOP-JG7N5D1:~$ python3 -V #2.查看当前系统的python3 环境版本 必须大于 Python3.7 以上 
sudo apt-get install python3-pip #3.安装python3的pip3工具 ，作用管理第三方软件包
pip3 install zhipuai #4.安装智普的ChatGLM SDK库 
将ChatGLM模型文件和相关权重放置在项目目录下。
在chatglm_model.py中编写代码来加载和初始化ChatGLM模型。
3.实现串口通信
在iat_online_sample.c中编写代码来配置和初始化串口通信。
实现串口数据的读取和发送功能，用于与用户进行交互。
4.集成模型推理和串口通信
编写C/C++代码，调用ChatGLM模型提供的API接口，实现具体的应用功能。
根据需求，可以在应用中集成其他硬件外设或传感器，实现更加丰富的功能。
在主程序中（例如iat_online_sample.c）集成ChatGLM模型推理和串口通信的逻辑。
当接收到客户端通过串口发送的消息时，使用ChatGLM模型进行推理并生成回复。
将生成的回复通过串口发送回用户。
5.测试和调试
使用交叉编译工具链编译生成适用于GEC6818开发板的可执行文件。
将生成的可执行文件烧录至GEC6818开发板，并进行实际测试
在开发板上运行程序clien.c和iat_online_sample.c，并通过串口终端或网线发送测试消息。
观察程序是否能够正确接收消息、进行模型推理并生成回复。
根据需要进行调试和优化。
五、注意事项
ChatGLM模型可能较大，需要根据gec6818开发板的存储和计算能力进行适当的调整或优化。
串口通信的参数（如波特率、数据位、停止位等）需要根据实际硬件和通信协议进行配置。
在开发过程中，注意保持代码的清晰和可维护性，便于后续的修改和扩展。
六、参考资料
ChatGLM官方文档：https://github.com/THUDM/ChatGLM
GEC6818开发板相关文档：https://www.gec.cn/product/gec6818.html
交叉编译工具链安装教程：https://www.cnblogs.com/shixiangwuyun/p/10265015.html
七、联系方式
如有任何疑问或建议，请通过以下方式联系我们：
QQ：2713739132 / 3457145303 
GitHub仓库：项目GitHub仓库链接

