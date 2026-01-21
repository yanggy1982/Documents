
# UI-TARS系列模型

## 1、UI-STARS系列简介

## 2、模型部署

### 2.1、模型部署要求

| 模型规模 | 最低配置 | 推荐配置 | 推理速度 |
|------|------|------|------|
| 7B   | 16GB VRAM (A10)  | 24GB VRAM (A100) | ~80-120 | 
| 72B  | 80GB VRAM (2xA100) | 160GB VRAM (4xA100) | ~30-50 |


### 2.2、vLLM部署

```shell
# 使用vLLM部署（推荐）
pip install vllm==0.6.6
python -m vllm.entrypoints.openai.api_server \
    --served-model-name ui-tars \
    --model /path/to/ui-tars-1.5-7b \
    --limit-mm-per-prompt image=5 \
    -tp 1  # 7B模型使用1卡，72B模型建议4卡
 
# 测试API连接
curl http://localhost:8000/v1/models
```