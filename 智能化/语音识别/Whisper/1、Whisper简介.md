
# Whisper简介

## 1、简介

### 1.1、什么是Whisper

&nbsp;&nbsp;&nbsp;&nbsp;Whisper是由OpenAI于2022年推出的开源语音识别模型，其核心创新在于采用”弱监督学习”框架，通过海量多语言数据训练出具备强大泛化能力的语音处理系统。

&nbsp;&nbsp;&nbsp;&nbsp;**官网地址**：https://github.com/openai/whisper

### 1.2、Whisper的优势

&nbsp;&nbsp;&nbsp;&nbsp;与传统ASR（自动语音识别）模型相比，Whisper展现出三大显著优势：

1. **多语言统一建模**：支持99种语言的识别与翻译，包括低资源语言（如斯瓦希里语、乌尔都语），且无需针对特定语言进行微调。例如在医疗场景中，可准确识别非洲方言的医学术语。


2. **鲁棒性设计**：通过在包含背景噪音、口音变体、非标准发音的数据上训练，模型对实际场景中的音频干扰具有天然抗性。测试显示，在60dB背景噪音下仍保持87%的准确率。


3. **端到端架构**：采用Transformer编码器-解码器结构，直接处理原始音频波形，省去传统流程中的特征提取、声学模型等复杂模块。这种设计使模型能够自主学习音频特征表示，在WSJ（华尔街日报）数据集上达到5.7%的词错率（WER）。

### 1.3、模型选择策略

| 模型规模 | 参数量 | 适用场景        | 推荐硬件 | 内存或显存 |
|------|-----|-------------| ------ | -------- |
| tiny | 39M | 移动端/嵌入设备    | CPU/集成显卡 | |
| base | 74M | 实时转写（短音频）   | 入门级GPU | |
| small | 244M | 通用场景（中长音频）  | 中端GPU | |
| large | 1550M | 高精度需求（医疗/法律）  | 旗舰级GPU | |
| large-v3 | 1550M | 最新优化版（支持VAD）  | 旗舰级GPU | |

## 2、安装

### 2.1、系统要求

#### 一、基础硬件配置

- **CPU方案**：推荐Intel i7-12700K及以上（需支持AVX2指令集），内存≥16GB


- **GPU方案**：NVIDIA RTX 3060（8GB显存）起，建议RTX 4090（24GB显存）处理长音频


- **存储需求**：基础模型约15GB（tiny-en）至155GB（large-v3），建议预留双倍空间用于中间文件

#### 二、环境配置要点

- **操作系统**：Ubuntu 22.04 LTS（推荐）或Windows 11（需WSL2）


- **Python环境**：3.10.x版本（与PyTorch 2.0+兼容性最佳）


- **CUDA工具包**：11.7版本（匹配PyTorch 2.0的CUDA版本）


- **依赖管理**：建议使用conda创建独立环境


### 2.2、环境创建及依赖安装

#### 一、创建环境

```shell
conda create -n whisper python=3.12
conda activate whisper
```

#### 二、依赖安装

```shell
pip install openai-whisper

# 可选
pip install torch 

# 可选
pip install ffmpeg-python
```

依赖说明：

- **openai-whisper**：官方封装库，提供模型加载与推理接口

- **torch**：深度学习框架，支持GPU加速

- **ffmpeg-python**：音频格式转换工具

### 2.3、手动安装

#### 一、安装依赖

```shell
git clone https://github.com/openai/whisper.git
cd whisper
pip install -e .
```

#### 二、手动下载模型

```shell
# 以medium模型为例
wget https://openaipublic.blob.core.windows.net/main/models/medium.pt
```




















