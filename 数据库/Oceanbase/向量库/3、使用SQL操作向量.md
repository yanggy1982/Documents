
# 使用SQL操作系统向量

## 1、创建向量表

### 1.1、创建稠密向量列和索引

```sql
-- 创建稠密向量列和索引
CREATE TABLE t1(
    id INT PRIMARY KEY, 
    doc VARCHAR(200),
    embedding VECTOR(3), 
    VECTOR INDEX idx1(embedding) WITH (distance=L2, type=hnsw)
);
```

### 1.2、创建稀疏向量列和内存稀疏索引

```sql
-- 创建稀疏向量列和内存稀疏索引
CREATE TABLE t2 (
    c1 INT, 
    c2 SPARSEVECTOR
    VECTOR INDEX idx2(c2) WITH (distance=inner_product, type=sindi)
);
```

## 2、插入数据

```sql
INSERT INTO t1
  VALUES (1, '苹果', '[1.2,0.7,1.1]'),
         (2, '香蕉', '[0.6,1.2,0.8]'),
         (3, '橙子','[1.1,1.1,0.9]'),
         (4, '胡萝卜', '[5.3,4.8,5.4]'),
         (5, '菠菜', '[4.9,5.3,4.8]'),
         (6, '西红柿','[5.2,4.9,5.1]');
```

## 3、搜索

```sql
SELECT id, doc FROM t1
ORDER BY l2_distance(embedding, '[0.9, 1.0, 0.9]')
APPROXIMATE LIMIT 3;
```





