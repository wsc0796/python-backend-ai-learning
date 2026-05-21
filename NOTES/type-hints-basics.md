# Python 类型注解基础

## 语法规则

```python
# 变量注解：变量名: 类型 = 值
name: str = "张三"
age: int = 20

# 函数参数 + 返回类型
def greet(name: str, age: int) -> str:
    return f"{name} 今年 {age} 岁"
```

## 联合类型（Python 3.10+）

```python
# 一个字段可能是多种类型
content: str | None = None      # 字符串或空
value: int | str = 42           # 整数或字符串
```

## 在 Pydantic 中的应用

```python
class NoteCreate(BaseModel):
    content: str                    # 必填：创建必须传

class NoteUpdate(BaseModel):
    content: str | None = None      # 可选：不传就不改
```

## 常见类型速查

```python
name: str = "abc"
count: int = 42
ratio: float = 3.14
done: bool = True

items: list[int] = [1, 2, 3]
mapping: dict[str, int] = {"a": 1}
```

## 重点

- 类型注解**不影响运行**，Python 不会因为类型不匹配报错
- 它给 IDE、mypy、Pydantic 用的
- Pydantic 用类型做自动校验 + JSON Schema 生成
