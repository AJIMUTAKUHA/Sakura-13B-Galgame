<div align="center">
<h1>
  Sakura-13B-Galgame
</h1>
</div>

<p align="center">
🤗 <a href="https://huggingface.co/sakuraumi/Sakura-13B-Galgame" target="_blank">Hugging Face</a> • 🤖 <a href="https://www.modelscope.cn/models/sakuraumi/Sakura-13B-Galgame" target="_blank">ModelScope</a>
</p>

# 介绍

基于OpenBuddy(v0.1-v0.4), Qwen-14B(v0.7,v0.9)和Baichuan2-13B(v0.5,v0.8)构建，在通用日文语料与轻小说/Galgame等领域的中日语料上进行微调，旨在提供性能接近GPT3.5且完全离线的Galgame/轻小说翻译大语言模型. 新建了[TG交流群](https://t.me/+QMDKZyO9GV1kNDA1)，欢迎交流讨论。

**如果使用模型翻译并发布，请在最显眼的位置标注机翻！！！！！开发者对于滥用本模型造成的一切后果不负任何责任。**

**对于模型翻译的人称代词问题（错用，乱加，主宾混淆，男女不分等）和上下文理解问题，如果有好的想法或建议，欢迎提issue！**

### 快速开始
 - [python部署教程](https://sakura.srpr.moe)
 - [llama.cpp一键包教程](https://books.fishhawk.top/forum/656d60530286f15e3384fcf8)
 - [autodl租显卡部署教程](https://books.fishhawk.top/forum/65719bf16843e12bd3a4dc98)

### News

1. 预览版v0.9.0pre2模型发布。该版本模型只是预览版本，目前可能仍存在问题。修复了上一预览版本短文本退化的问题。

2. **网站：[轻小说机翻机器人](https://books.fishhawk.top/)已接入Sakura模型(v0.8-4bit)，站内有大量模型翻译结果可供参考。你也可以自行部署模型并使用该网站生成机翻，目前已经支持v0.8与v0.9模型，且提供了llama.cpp一键包。**
  
   轻小说机翻机器人网站是一个自动生成轻小说机翻并分享的网站。你可以浏览日文网络小说，或者上传Epub/Txt文件，并生成机翻。

3. **[LunaTranslator](https://github.com/HIllya51/LunaTranslator)已经支持Sakura API，可以通过本地部署API后端，并在LunaTranslator中配置Sakura API来使用Sakura模型翻译Galgame。**

   LunaTranslator是一个Galgame翻译工具，支持剪贴板、OCR、HOOK，支持40余种翻译引擎。

### 模型下载：
|   版本  | 全量模型 | 8-bit量化 | 4-bit量化 | 3-bit量化 | GGUF | AWQ
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| 20231026-v0.8 | 🤗 [Sakura-13B-LNovel-v0.8](https://huggingface.co/SakuraLLM/Sakura-13B-LNovel-v0.8) | 🤗 [Sakura-13B-LNovel-v0_8-8bit](https://huggingface.co/SakuraLLM/Sakura-13B-LNovel-v0_8-8bit) | 🤗 [Sakura-13B-LNovel-v0_8-4bit](https://huggingface.co/SakuraLLM/Sakura-13B-LNovel-v0_8-4bit) | 🤗 [Sakura-13B-LNovel-v0_8-3bit](https://huggingface.co/SakuraLLM/Sakura-13B-LNovel-v0_8-3bit) | 🤗 [Sakura-13B-LNovel-v0_8-GGUF](https://huggingface.co/SakuraLLM/Sakura-13B-LNovel-v0.8-GGUF) | 🤗 [Sakura-13B-LNovel-v0_8-AWQ](https://huggingface.co/SakuraLLM/Sakura-13B-LNovel-v0_8-AWQ) |
| 20231125-v0.9.0pre2 | 🤗 [Sakura-13B-LNovel-v0.9.0pre2](https://huggingface.co/SakuraLLM/Sakura-13B-LNovel-v0.9.0pre2) | - | - | - | 🤗 [Sakura-13B-LNovel-v0.9.0pre2-GGUF](https://huggingface.co/SakuraLLM/Sakura-13B-LNovel-v0.9.0pre2-GGUF) | - |

目前仍为实验版本，翻译质量在文风与流畅度上强于GPT-3.5，但词汇量逊于GPT-3.5. 个人使用推荐GPT4.

# 显存需求

下面的表格显示了使用不同量化和不同格式的模型时显存占用的大小。如果你的显卡显存不满足上述需求，可以尝试同时使用CPU与GPU进行推理。

- llama.cpp GGUF模型（使用v0.9.0pre1模型进行测试，v0.8模型与其类似）

|  模型量化类型  | 模型大小 | 推荐显存大小 |
|:-------:|:-------:|:-------:|
| fp16 | 26.3G | 超出游戏显卡显存范围 |
| Q8_0 | 14G | 24G |
| Q6_K | 11.4G | 20G |
| Q5_K_M | 10.1G | 16G |
| Q4_K_M | 8.8G | 16G |
| Q3_K_M | 7.2G | 16G |
| Q2_K | 6.1G | 12G |

- transformers autogptq模型（使用v0.8版本进行测试）

|  模型量化类型 | 推理显存(ctx约600) | 推理显存(ctx约1800) |
|:-------:|:-------:|:-------:|
| 全量 | 超出游戏显卡显存范围  | 超出游戏显卡显存范围  |
| 8bit | 21.1G | 23.4G |
| 4bit | 14.9G | 17.4G |
| 3bit | 13.7G | 15.5G |

# 使用

## Docker部署

详见分支`dev_server`中的[README.docker.md](https://github.com/SakuraLLM/Sakura-13B-Galgame/blob/dev_server/README.docker.md)

## 本地部署

首先将本仓库拉取到本地。

- 启动API服务

切换到`dev_server`分支，该分支提供了API接口（感谢[KurikoMoe](https://github.com/kurikomoe)），用以提供API服务，以接入其他程序。

```bash
# 参数说明：
# 模型相关
# --model_name_or_path：模型本地路径或者huggingface仓库id。
# --model_version：模型版本，本仓库README表格中即可查看。可选范围：['0.1', '0.4', '0.5', '0.7', '0.8']
# --use_gptq_model：如果模型为gptq量化模型，则需加此项；如是全量模型，则不需要添加。
# --trust_remote_code：是否允许执行外部命令（对于0.5，0.7，0.8版本模型需要加上这个参数，否则报错。
# --llama：如果你使用的模型是llama家族的模型（对于0.1，0.4版本），则需要加入此命令。
# API服务相关
# --listen：指定要监听的IP和端口，格式为<IP>:<Port>，如127.0.0.1:5000。默认为127.0.0.1:5000
# --auth：使用认证，访问API需要提供账户和密码。
# --no-auth：不使用认证，如果将API暴露在公网可能会降低安全性。
# --log：设置日志等级。
# 下面为一个使用v0.8-4bit模型，同时不使用认证，监听127.0.0.1:5000的命令示例。
# 这里模型默认从huggingface拉取，如果你已经将模型下载至本地，可以将--model_name_or_path参数的值指定为本地目录。
python server.py --model_name_or_path SakuraLLM/Sakura-13B-LNovel-v0_8-4bit --use_gptq_model --model_version 0.8 --trust_remote_code --no-auth
```

- 翻译Epub文件

仓库提供了脚本`translate_epub.py`（感谢[CjangCjengh](https://github.com/CjangCjengh)），用于翻译Epub格式的小说。使用示例如下：

```bash
# 参数说明：
# --model_name_or_path：模型本地路径或者huggingface仓库id。
# --model_version：模型版本，本仓库README表格中即可查看。可选范围：['0.1', '0.4', '0.5', '0.7', '0.8']
# --use_gptq_model：如果模型为gptq量化模型，则需加此项；如是全量模型，则不需要添加。
# --text_length：文本分块的最大单块文字数量。
# --data_path：日文原文Epub小说文件路径。
# --data_folder：批量翻译Epub小说时，小说所在的文件夹路径
# --output_folder：翻译后的Epub文件输出路径（注意是文件夹路径）。
# --translate_title：是否翻译Epub文件的文件名（添加则翻译）
# --trust_remote_code：是否允许执行外部命令（对于0.5，0.7，0.8版本模型需要加上这个参数，否则报错。
# --llama：如果你使用的模型是llama家族的模型（对于0.1，0.4版本），则需要加入此命令。
# 以下为一个例子
python translate_epub.py \
    --model_name_or_path SakuraLLM/Sakura-13B-LNovel-v0_8-4bit \
    --trust_remote_code \
    --model_version 0.8 \
    --use_gptq_model \
    --text_length 512 \
    --data_path novel.epub \
    --output_folder output
```

- 翻译纯文本

仓库提供了脚本`translate_novel.py`，用于翻译轻小说等纯文本格式，支持输出中日对照文本。使用示例如下：

```bash
# 参数说明：
# --model_name_or_path：模型本地路径或者huggingface仓库id。
# --model_version：模型版本，本仓库README表格中即可查看。可选范围：['0.1', '0.4', '0.5', '0.7', '0.8']
# --use_gptq_model：如果模型为gptq量化模型，则需加此项；如是全量模型，则不需要添加。
# --text_length：文本分块的最大单块文字数量。每块文字量将在text_length/2至text_length内随机选择。
# --compare_text：是否需要输出中日对照文本，如需要，则需加此项；如不需要则不要添加。
# --data_path：日文原文文件路径
# --output_path：翻译(或对照)文本输出文件路径
# --trust_remote_code：是否允许执行外部命令（对于0.5，0.7，0.8版本模型需要加上这个参数，否则报错。
# --llama：如果你使用的模型是llama家族的模型（对于0.1，0.4版本），则需要加入此命令。
# 以下为一个例子
python translate_novel.py \
    --model_name_or_path SakuraLLM/Sakura-13B-LNovel-v0_8-4bit \
    --trust_remote_code \
    --model_version 0.8 \
    --use_gptq_model \
    --text_length 512 \
    --data_path data.txt \
    --output_path data_translated.txt \
    --compare_text
```

# 日志

`20231125`: 上传第六版模型预览，改善数据集质量与格式，使用Qwen-14B-Chat模型进行继续预训练+微调，增加数据集。

`20231026`：上传第五版模型`sakura-13b-2epoch-3.8M-1025-v0.8`，改善数据集质量与格式，修复之前版本模型无法正确解析\n的问题，使用Baichuan2-13B-Chat模型进行微调。

`20231011`：上传第四版模型`sakura-14b-2epoch-4.4M-1003-v0.7`，改用QWen-14B-Chat模型进行微调，针对较长文本进行优化，增加数据集。

`20230918`：上传第三版模型的8bits量化版`sakura-13b-2epoch-2.6M-0917-v0.5-8bits`。

`20230917`：上传第三版模型`sakura-13b-2epoch-2.6M-0917-v0.5`，改用Baichuan2-13B-Chat模型进行微调，翻译质量有所提高。

`20230908`：上传第二版模型`sakura-13b-1epoch-2.6M-0903-v0.4`，使用Galgame和轻小说数据集进行微调，语法能力有所提高。感谢[CjangCjengh](https://github.com/CjangCjengh)大佬提供轻小说数据集。

`20230827`：上传第一版模型`sakura-13b-2epoch-260k-0826-v0.1`

# 模型详情

## 描述

### v0.1-v0.4

- Finetuned by [SakuraUmi](https://github.com/pipixia244)
- Finetuned on [Openbuddy-LLaMA2-13B](https://huggingface.co/OpenBuddy/openbuddy-llama2-13b-v8.1-fp16)
- Base model: [LLaMA2-13B](https://huggingface.co/meta-llama/Llama-2-13b-chat-hf)
- Languages: Chinese/Japanese

### v0.5

- Finetuned by [SakuraUmi](https://github.com/pipixia244)
- Finetuned on [Baichuan2-13B-Chat](https://huggingface.co/baichuan-inc/Baichuan2-13B-Chat)
- Base model: [Baichuan2-13B-Base](https://huggingface.co/baichuan-inc/Baichuan2-13B-Base)
- Languages: Chinese/Japanese

### v0.7

- Finetuned by [SakuraUmi](https://github.com/pipixia244)
- Finetuned on [Qwen-14B-Chat](https://huggingface.co/Qwen/Qwen-14B)
- Base model: [Qwen-14B](https://huggingface.co/Qwen/Qwen-14B)
- Languages: Chinese/Japanese

### v0.8

- Finetuned by [SakuraUmi](https://github.com/pipixia244)
- Finetuned on [Baichuan2-13B-Chat](https://huggingface.co/baichuan-inc/Baichuan2-13B-Chat)
- Base model: [Baichuan2-13B-Base](https://huggingface.co/baichuan-inc/Baichuan2-13B-Base)
- Languages: Chinese/Japanese

## 版本

### v0.8

数据集：约0.25B字数的轻小说/Galgame中日平行语料

微调方式：全参数

微调epoch数：2

参数量：13.9B

### v0.7

数据集：约0.3B字数的轻小说/Galgame中日平行语料

微调方式：全参数

微调epoch数：2

参数量：14B

### v0.5

数据集：约0.17B字数的轻小说/Galgame中日平行语料

微调方式：全参数

微调epoch数：2

参数量：13B

### v0.4

数据集：约0.17B字数的轻小说/Galgame中日平行语料

微调方式：全参数

微调epoch数：1

参数量：13B

### v0.1

数据集：约10M字数的Galgame中日平行语料

微调方式：全参数

微调epoch数：2

参数量：13B

## 效果

- Galgame

  TBD
  
- 轻小说

  网站：[轻小说机翻机器人](https://books.fishhawk.top/)已接入Sakura模型(v0.8-4bit)，站内有大量模型翻译的轻小说可供参考。

# 推理

- Galgame翻译的prompt构建：

  - v0.1

    ```python
    input_text = "" # 用户输入
    query = "将下面的日文文本翻译成中文：" + input_text
    prompt = "Human: \n" + query + "\n\nAssistant: \n"
    ```
    
  - v0.4

    ```python
    input_text = "" # 用户输入
    query = "将下面的日文文本翻译成中文：" + input_text
    prompt = "User: " + query + "\nAssistant: "
    ```

  - v0.5与v0.8

    ```python
    input_text = "" # 用户输入
    query = "将下面的日文文本翻译成中文：" + input_text
    prompt = "<reserved_106>" + query + "<reserved_107>"
    ```
    
  - v0.7
    参考Qwen-14B-Chat的prompt构造方式：[这里](https://huggingface.co/Qwen/Qwen-14B-Chat/blob/5188dfeb4ff175705aa3a84ef9d616c70dea029b/qwen_generation_utils.py#L119)和[这里](https://github.com/hiyouga/LLaMA-Efficient-Tuning/blob/5310e4d1829f36619c8f224d09ec15eeaf7a4877/src/llmtuner/extras/template.py#L546)


- 推理与解码参数：

| 参数 | 值 |
| ---- | ---- |
| temperature | 0.1 |
| top p | 0.3 |
| do sample | True |
| beams number | 1 |
| repetition penalty | 1 |
| max new token | 512 |
| min new token | 1 |

- 量化：

根据transformers文档中给出的AutoGPTQ量化教程自行量化，或使用我们已经量化好的模型。

使用量化模型推理的示例代码：

```python
from transformers import AutoTokenizer, GenerationConfig
from auto_gptq import AutoGPTQForCausalLM

path = "path/to/your/model"
text = "" #要翻译的文本

generation_config = GenerationConfig.from_pretrained(path)
tokenizer = AutoTokenizer.from_pretrained(path, use_fast=False, trust_remote_code=True)
model = AutoGPTQForCausalLM.from_quantized(path, device="cuda:0", trust_remote_code=True)

response = tokenizer.decode(model.generate(**tokenizer(f"<reserved_106>将下面的日文文本翻译成中文：{text}<reserved_107>", return_tensors="pt").to(model.device), generation_config=generation_config)[0]).replace("</s>", "").split("<reserved_107>")[1]
print(response)
```

# 微调

流程与LLaMA2(v0.1-v0.4)/Baichuan2(v0.5与v0.8)/Qwen14B(v0.7)一致，prompt构造参考推理部分

# 后续工作

1. 优化SFT数据集，构建PT数据集
2. 在Base model基础上进行继续预训练（正在进行）

# 致谢

- [CjangCjengh](https://github.com/CjangCjengh)

- [ryank231231](https://github.com/ryank231231)

- [KurikoMoe](https://github.com/kurikomoe)

- [FishHawk](https://github.com/FishHawk)

- [K024](https://github.com/K024)

- [minaduki-sora](https://github.com/minaduki-sora)

- [Kimagure7](https://github.com/Kimagure7)

- [YYF233333](https://github.com/YYF233333)

# Copyright Notice

This model is built upon Meta's LLaMA series of models and is subject to Meta's licensing agreement.

This model is intended for use only by individuals who have obtained approval from Meta and are eligible to download LLaMA.

If you have not obtained approval from Meta, you must visit the https://ai.meta.com/llama/ page, read and agree to the model's licensing agreement, submit an application, and wait for approval from Meta before downloading the model from this page.
