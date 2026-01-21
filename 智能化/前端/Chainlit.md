
# Chainlit

## 1、Chainlit简介

### 1.1、什么是Chainlit

- Chainlit是一个开源的异步Python框架，专为构建可扩展的对话式 AI 或代理应用而设计。它允许开发者在几分钟内快速搭建生产级的对话式 AI 应用，而不需要花费数周时间。
- Chainlit提供了丰富的文档和示例，帮助开发者快速上手。通过 Chainlit，开发者可以轻松集成各种工具和服务，如 OpenAI、LangChain、LlamaIndex 等，从而构建功能强大的对话式 AI 应用。

### 1.2、Chainlit的主要功能

- **快速构建**：通过简单的 Python 代码，开发者可以快速构建对话式 AI 应用。
- **异步支持**：基于 Python 的异步框架，确保应用的高效运行。
- **工具集成**：支持与多种工具和服务（如 OpenAI、LangChain、LlamaIndex）的无缝集成。
- **实时交互**：提供实时消息处理功能，用户输入消息后，应用可以立即响应。

### 1.3、相关资源

- **GitHub仓库**：https://github.com/chainlit/chainlit
- **项目文档**：https://docs.chainlit.io
- **Chainlit帮助**：https://help.chainlit.io/
- **Cookbook示例**：https://github.com/Chainlit/cookbook

## 2、安装和运行

### 2.1、安装

```shell
pip install chainlit
chainlit hello
```

### 2.2、开发版本安装

```shell
pip install git+https://github.com/Chainlit/chainlit.git#subdirectory=backend/
```

## 3、Chainlit使用

### 3.1、快速入门

- 代码如下 demo.py

```python
import chainlit as cl


@cl.step(type="tool")
async def tool():
    # 模拟工具操作
    await cl.sleep(2)
    return "工具返回的响应！"


@cl.on_message  
async def main(message: cl.Message):
    """
    当用户在 UI 中输入消息时，此函数将被调用。
    它会先发送工具的中间响应，然后发送最终答案。

    参数:
        message: 用户的消息。

    返回:
        无。
    """

    # 调用工具
    tool_res = await tool()

    await cl.Message(content=tool_res).send()
```

- 运行代码

```shell
chainlit run demo.py -w
```



























