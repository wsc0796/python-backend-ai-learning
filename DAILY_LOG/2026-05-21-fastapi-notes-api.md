# 2026-05-21 FastAPI Notes API

## 今天做了什么

1. **计算机网络入门：** 五层模型、TCP vs UDP、三次握手/四次挥手
2. **FastAPI 实战：** 给 notes-api 加了 PATCH 更新 + GET 搜索接口，共 6 个端点
3. **TestClient 测试：** 11 个测试覆盖正常 + 边界情况
4. **基础补全：** 类型注解、联合类型 (`| None`)、类与对象基础

## 关键理解

### FastAPI 请求全链路

```
浏览器发请求
  → 路径/查询参数绑定
  → Depends 执行（在函数体之前）
  → 注入 service 对象
  → 执行函数体
  → return 结果 → response_model 序列化 → HTTP 响应
```

### 核心知识点

| 概念 | 理解 |
|------|------|
| PATCH vs PUT | PATCH 只改传了的字段，`exclude_unset=True` + `\| None` |
| 422 vs 404 | 422 格式错，404 资源不存在 |
| Depends 时机 | 路由函数执行之前 |
| 分层原则 | main 只管 HTTP，repository 管数据 |

## 遇到的问题

- `content: str | None` 语法看不懂 → 补了类型注解基础
- `JsonNoteRepository("notes.json")` 不理解 → 补了类与对象
- 测试文件的 TestClient 模式陌生 → 读了 11 个测试用例

## 明天计划

1. TestClient 正式化 + 分页
2. 独立改代码检验
3. Hot100 恢复手感
