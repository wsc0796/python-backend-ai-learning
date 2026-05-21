# FastAPI 请求调用链

一个请求从进来到回去，经过的全部步骤：

```
浏览器发 GET /notes/3?q=hello
  ↓
① 路径参数绑定：{note_id} → 3（定位资源）
   查询参数绑定：?q=hello → q="hello"（过滤/配置）
  ↓
② Depends(get_note_service) 执行 ← 在函数体之前
  ↓
③ 拿到 service 对象，注入给函数参数
  ↓
④ 执行函数体：service.get_note(note_id)
  ↓
⑤ return NoteRead 对象
  ↓
⑥ FastAPI 根据 response_model 序列化成 JSON
  ↓
⑦ 返回 HTTP 响应
```

## 路径参数 vs 查询参数

| 类型 | 示例 | 作用 | 函数写法 |
|------|------|------|---------|
| 路径参数 | `/notes/{id}` | 定位资源 | `def get(id: int)` |
| 查询参数 | `?q=hello&limit=10` | 过滤/分页 | `def search(q: str)` |

## HTTP 状态码速记

| 状态码 | 含义 | 场景 |
|--------|------|------|
| 200 | 成功 | 查询/更新成功 |
| 201 | 创建成功 | POST 创建 |
| 204 | 删除成功 | DELETE 无返回体 |
| 404 | 资源不存在 | id=99999 不存在 |
| 422 | 数据格式不对 | content 为空 |

## 五分层的职责

```
main.py          ← HTTP 路由 + 参数提取 + 状态码
dependencies.py  ← DI 组装车间（唯一的创建点）
service.py       ← 业务逻辑（异常定义）
repository.py    ← 数据持久化（文件/数据库）
models.py        ← 输入/输出数据契约
```
