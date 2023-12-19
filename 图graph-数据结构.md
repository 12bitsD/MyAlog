# 图（graph）

---

> 图由节点（node）和边（edge）组成，一个节点可以与多个节点连接并且可以形成cycle。
>
> 图用于模拟数据之间的相连
> 节点（node）之间可以存在方向（有向图 direction graph），也可以没有（无向图 undirected graph）
>
> 边（edge）可以存在权重（weight graph）= 消耗成本

## 实现图列表

图拆分成边和node，分别可以用以下数据结构进行表示

1. 数集（set）+dictionary+tuple

```python
#node;
node = {a,b,c}
#edges
D={ a : {b,c} }
D(a) = {b,c}
#weight
D= { a:{ (b,2),(c,2) } }
```



2. 列表（list）/(list+dictionary) +tuple

```python
node=["a","b","c"]

D=[ ["b","c"],
	["a","c"],
	["a","b"] ]
#weight
D=[ [('b',2),('c',2)],
  		…… ,
  	   [('a',2),('c',2)] ]

```

weight最好用tuple实现

## 图矩阵（Matrix）

```python
D=[
[1, 0, 1, 1, 0, 0],

[1, 1, 0, 1, 0, 1],

[0, 1, 1, 0, 1, 0],

[0, 0, 0, 1, 0, 1],

[1, 0, 1, 0, 1, 0]
]
#0表示没有connection，1表示connected
```

