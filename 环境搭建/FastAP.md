
# FastAPI 环境搭建

## 1、创建conda环境

```shell
conda create -n FastAPIStudy python=3.12

conda activate FastAPIStudy
```

## 2、安装依赖包

### 2.1、安装基础包

```shell
pip install python-dotenv

pip install loguru

pip install pydantic_settings
```

### 2.2、安装FastAPI包

```shell
pip install fastapi

pip install uvicorn

pip install sse-starlette

pip install dependency-injector
```

### 2.3、选装包

```shell
pip install SQLAlchemy
```