
# 使用Python操作向量

## 1、简介

pyobvector 是 OceanBase 向量存储的 Python SDK，基于 SQLAlchemy，基本兼容 Milvus API。

## 2、安装

```shell
pip install -U pyobvector
```

## 3、用法

pyobvector 支持两种模式：

- **Milvus 兼容模式**：用 MilvusLikeClient 类提供的类似于 Milvus API 的方式来使用向量存储。


- **SQLAlchemy 混合模式**：使用 ObVecClient 类提供的向量存储功能，并用 SQLAlchemy 库执行关系数据库语句。在这种模式下，可以将 pyobvector 视为 SQLAlchemy 的扩展。


## 4、Milvus 兼容模式

### 4.1、建立连接

```python
from pyobvector import *

# 创建客户端
client = MilvusLikeClient(uri="192.168.180.100:2881", user="root@test", password="Happy123#", db_name="tongtong-db")
```

### 4.2、创建集合

```python
from pyobvector import *


# 创建客户端
client = MilvusLikeClient(uri="192.168.180.100:2881", user="root@test",password="Happy123#", db_name="tongtong-db")

fields = [
    FieldSchema(
        name="id",
        dtype=DataType.INT64,
        is_primary=True,
        auto_id=True,
    ),
    FieldSchema(name="embedding", dtype=DataType.FLOAT_VECTOR, dim=64),
    FieldSchema(name="metadata", dtype=DataType.JSON),
]

index_params = MilvusLikeClient.prepare_index_params()
index_params.add_index(
    field_name="embedding",
    index_name="embedding_idx",
    index_type=VecIndexType.HNSW,
    distance="l2",
    m=16,
    ef_construction=256,
)

schema = CollectionSchema(fields)
table_name = "vector_search"
client.create_collection(table_name, schema=schema, index_params=index_params)
```

### 4.3、批量插入数据

```python
from pyobvector import *
import random

# 创建客户端
client = MilvusLikeClient(uri="192.168.180.100:2881", user="root@test", password="Happy123#", db_name="tongtong-db")

table_name = "vector_search"

random.seed(20241023)

batch_size = 100
batch = []
for i in range(1000):
    batch.append(
        {
            "embedding": [random.uniform(-1, 1) for _ in range(64)],
            "metadata": {"idx": i},
        }
    )
    if len(batch) == batch_size:
        client.insert(table_name, data=batch)
        batch = []

if len(batch) > 0:
    client.insert(table_name, data=batch)
```

### 4.4、检索

```python
from pyobvector import *
import random

# 创建客户端
client = MilvusLikeClient(uri="192.168.180.100:2881", user="root@test", password="Happy123#", db_name="tongtong-db")

table_name = "vector_search"

target_data = [random.uniform(-1, 1) for _ in range(64)]
res = client.search(
    collection_name=table_name,
    data=target_data,
    anns_field="embedding",
    limit=5,
    output_fields=["id", "metadata"],
)
print(res)
```


## 5、SQLAlchemy 混合模式

### 5.1、建立连接

```python
from pyobvector import *

# 创建客户端
client = ObVecClient(uri="192.168.180.100:2881", user="root@test",password="Happy123#", db_name="tongtong-db")
```

### 5.2、创建集合

```python
from pyobvector import *
from sqlalchemy import Column, Integer, JSON

# 创建客户端
client = ObVecClient(uri="192.168.180.100:2881", user="root@test",password="Happy123#", db_name="tongtong-db")

cols = [
    Column("id", Integer, primary_key=True, autoincrement=True),
    Column("embedding", VECTOR(64)),
    Column("metadata", JSON),
]
table_name = "vector_test3"
client.create_table(table_name, columns=cols)
print(f"Table {table_name} created")
client.create_index(
    table_name,
    is_vec_index=True,
    index_name="embedding_idx",
    column_names=["embedding"],
    vidx_params="distance=l2, type=hnsw, lib=vsag",  # m=16, ef_construction=256
)
print(f"Index {table_name}.embedding_idx created")
```

### 5.3、批量插入数据

```python
from pyobvector import *
import random

# 创建客户端
client = ObVecClient(uri="192.168.180.100:2881", user="root@test",password="Happy123#", db_name="tongtong-db")

table_name = "vector_test3"
random.seed(20241023)

batch_size = 100
batch = []
for i in range(1000):
    batch.append(
        {
            "embedding": [random.uniform(-1, 1) for _ in range(64)],
            "metadata": {"idx": i},
        }
    )
    if len(batch) == batch_size:
        client.insert(table_name, data=batch)
        batch = []

if len(batch) > 0:
    client.insert(table_name, data=batch)
```

### 5.4、检索

```python
from pyobvector import *
import random
from sqlalchemy import func

# 创建客户端
client = ObVecClient(uri="192.168.180.100:2881", user="root@test",password="Happy123#", db_name="tongtong-db")

table_name = "vector_test3"
random.seed(20241023)

target_data = [random.uniform(-1, 1) for _ in range(64)]
res = client.ann_search(
    table_name,
    vec_data=target_data,
    vec_column_name="embedding",
    distance_func=func.l2_distance,
    topk=5,
    output_column_names=["id", "metadata"],
)
for r in res:
    print(r)
```




