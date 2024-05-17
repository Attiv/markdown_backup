> 简单整理一下如何使用 continue 扩展配合 ollama 让 VS Code  
> 支持本地运行的 LLM 实现 AI 代码补全  

简单整理一下如何使用 continue 扩展配合 ollama 让 VS Code  
支持本地运行的 LLM 实现 AI 代码补全  

## Requirements

- Ollama.ai
- continue.dev

## 在本地准备 LLM 运行环境

### Install Ollama

### On the Mac

下载 ollama app [https://ollama.com/download](https://ollama.com/download)  
运行即可  

### On Linux / WSL

### CPU Only

```Plain
docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```

### Nvidia GPU

安装 [Nvidia container toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html#installation)

Run Ollama inside a Docker container

```Plain
docker run -d --gpus=all -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```

### Install LLM Model

这里安装 [`starcoder:3b`](https://ollama.com/library/starcoder:3b)

### Mac

```Plain
ollama run starcoder:3b
```

### Docker

```Plain
docker exec -it ollama ollama run starcoder:3b
```

确保模型下载完成，并成功启动

[![](https://blog.osvlabs.com/wp-content/uploads/2024/03/Pasted-image-20240307210329.png)](https://blog.osvlabs.com/wp-content/uploads/2024/03/Pasted-image-20240307210329.png)

## 在 VSCode 安装 continue 扩展

VSCode Extension

### [配置  
Tab 自动补全  
](https://marketplace.visualstudio.com/items?item%3Ehttps://marketplace.visualstudio.com/items?itemName=Continue.continue%3C/a%3E%3Cbr%3E%20%3Cimg%20class=)

[在  
VS Code 扩展安装后，进入 “Settings” 点击箭头编辑 settings.json  
](https://marketplace.visualstudio.com/items?item%3Ehttps://marketplace.visualstudio.com/items?itemName=Continue.continue%3C/a%3E%3Cbr%3E%20%3Cimg%20class=)[  
在 JSON 配置中增加 tab auto complete 配置  
](https://marketplace.visualstudio.com/items?item%3Ehttps://marketplace.visualstudio.com/items?itemName=Continue.continue%3C/a%3E%3Cbr%3E%20%3Cimg%20class=)

[![](https://blog.osvlabs.com/wp-content/uploads/2024/03/Pasted-image-20240307205754.png)](https://blog.osvlabs.com/wp-content/uploads/2024/03/Pasted-image-20240307205754.png)

```Plain
[{
...
    "tabAutocompleteModel": {
        "title": "Tab Autocomplete Model",
        "provider": "ollama",
        "model": "starcoder:3b",
        "apiBase": "https://127.0.0.1:11434" // ollama api endpoint
    },

    "tabAutocompleteOptions": {
        "useCopyBuffer": false, //Determines whether the copy buffer will be considered when constructing the prompt. (Boolean)
        "maxPromptTokens": 400, //The maximum number of prompt tokens to use. A smaller number will yield faster completions, but less context. (Number)
        "prefixPercentage": 0.5 // The percentage of the input that should be dedicated to the prefix. (Number)
    },
    "continue.enableTabAutocomplete": true
}](https://marketplace.visualstudio.com/items?item>https://marketplace.visualstudio.com/items?itemName=Continue.continue</a><br>
<img class=)
```

[![](https://blog.osvlabs.com/wp-content/uploads/2024/03/Pasted-image-20240307210058.png)](https://blog.osvlabs.com/wp-content/uploads/2024/03/Pasted-image-20240307210058.png)

[测试](https://marketplace.visualstudio.com/items?item%3Ehttps://marketplace.visualstudio.com/items?itemName=Continue.continue%3C/a%3E%3Cbr%3E%20%3Cimg%20class=)  
———————————————————————————————————————————————–  

[使用  
VS Code 新建一个 Python，这里我们添加一个注释来获得城市天气并输出  
JSON  
](https://marketplace.visualstudio.com/items?item%3Ehttps://marketplace.visualstudio.com/items?itemName=Continue.continue%3C/a%3E%3Cbr%3E%20%3Cimg%20class=)[  
出现预览后可敲击 Tab 补全  
](https://marketplace.visualstudio.com/items?item%3Ehttps://marketplace.visualstudio.com/items?itemName=Continue.continue%3C/a%3E%3Cbr%3E%20%3Cimg%20class=)[  
除了  
](https://marketplace.visualstudio.com/items?item%3Ehttps://marketplace.visualstudio.com/items?itemName=Continue.continue%3C/a%3E%3Cbr%3E%20%3Cimg%20class=)[`starcoder-3b`](https://marketplace.visualstudio.com/items?item%3Ehttps://marketplace.visualstudio.com/items?itemName=Continue.continue%3C/a%3E%3Cbr%3E%20%3Cimg%20class=)[外，还可以选择](https://marketplace.visualstudio.com/items?item%3Ehttps://marketplace.visualstudio.com/items?itemName=Continue.continue%3C/a%3E%3Cbr%3E%20%3Cimg%20class=) [`starcoder-1b`](https://marketplace.visualstudio.com/items?item%3Ehttps://marketplace.visualstudio.com/items?itemName=Continue.continue%3C/a%3E%3Cbr%3E%20%3Cimg%20class=)[  
或者  
](https://marketplace.visualstudio.com/items?item%3Ehttps://marketplace.visualstudio.com/items?itemName=Continue.continue%3C/a%3E%3Cbr%3E%20%3Cimg%20class=)[`deepseek-1b`](https://marketplace.visualstudio.com/items?item%3Ehttps://marketplace.visualstudio.com/items?itemName=Continue.continue%3C/a%3E%3Cbr%3E%20%3Cimg%20class=) [这种更小的模型以提升速度。](https://marketplace.visualstudio.com/items?item%3Ehttps://marketplace.visualstudio.com/items?itemName=Continue.continue%3C/a%3E%3Cbr%3E%20%3Cimg%20class=) >  
本文由简悦 SimpRead 转码  

[![](https://blog.osvlabs.com/wp-content/uploads/2024/03/Pasted-image-20240307211141.png)](https://blog.osvlabs.com/wp-content/uploads/2024/03/Pasted-image-20240307211141.png)

[![](https://blog.osvlabs.com/wp-content/uploads/2024/03/Pasted-image-20240307211239.png)](https://blog.osvlabs.com/wp-content/uploads/2024/03/Pasted-image-20240307211239.png)