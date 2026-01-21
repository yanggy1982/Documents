
# LangGraph环境搭建

## 1、创建conda环境

```shell
conda create -n LangGraphStudy python=3.12

conda activate LangGraphStudy
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

#### 三、扩展包

- (三)、MCP

```shell
pip install langchain-mcp-adapters
```


### 2.3、安装LangChain

#### 一、基础包

```shell
pip install langchain-community
```

#### 二、模型包

参考LangChain的安装




