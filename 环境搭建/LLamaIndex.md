
## 1、创建conda环境

```shell
conda create -n LlamaIndexStudy python=3.12

conda activate LlamaIndexStudy
```

## 2、安装依赖包

### 2.1、基础包

```shell
pip install llama-index
```

### 2.2、模型包

```shell
pip install llama-index-llms-openai

pip install llama-index-llms-ollama

pip install llama-index-llms-langchain

pip install llama-index-llms-deepseek
```

### 2.3、embedding模型包

```shell
pip install llama-index-embeddings-ollama

pip install llama-index-embeddings-openai

pip install llama-index-embeddings-huggingface

pip install llama-index-embeddings-langchain

pip install llama-index-embeddings-fastembed

pip install fastembed
```

### 2.4、stores包

```shell
pip install llama-index-vector-stores-milvus
```
