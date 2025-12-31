
# LangChain&LangGraph环境搭建

## 1、创建conda环境

```shell
conda create -n LangChainStudy python=3.12

conda activate LangChainStudy
```

## 2、安装依赖包

### 2.1、基础包

```shell
pip install python-dotenv
```

### 2.2、安装LangGraph

#### 一、基础包

```shell
pip install langgraph
```

#### 二、checkpoint

```shell
pip install langgraph-checkpoint-postgres

pip install langgraph-checkpoint-mongodb

pip install langgraph-checkpoint-sqlite
```

### 2.3、安装LangChain

#### 一、基础包

```shell
pip install langchain

pip install langchain-community

pip install langchain-core
```

#### 二、模型包

```shell
pip install langchain-openai

pip install langchain-anthropic

pip install langchain-ollama

pip install langchain-deepseek

pip install langchain_huggingface

pip install sentence-transformers

pip install qianfan

pip install dashscope

pip install fastembed

pip install FlagEmbedding
```
