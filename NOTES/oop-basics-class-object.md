# Python 类与对象基础

## 核心认知

```
类（Class）   = 模具/配方
对象（Object）= 用模具造出来的实际产品
__init__     = "造这个产品需要准备什么"
self         = "这个产品自己"
对象.方法()   = "让这个产品做一件事"
```

## 语法

```python
class Dog:
    def __init__(self, name):      # 造狗的时候要给它一个名字
        self.name = name           # 存下来

    def bark(self):                # 狗会叫
        print(f"{self.name} 汪汪")

# 使用：类名(参数) = 造对象
d = Dog("旺财")    # 造一只名叫旺财的狗
d.bark()           # 让它叫
```

## 对应到实际项目

```python
# 笔记里的 Dog                             # 你的 JsonNoteRepository
class Dog:                                 class JsonNoteRepository:
    def __init__(self, name):                  def __init__(self, filename):
        self.name = name                           self.filename = filename

    def bark(self):                              def list_notes(self):
        print(f"{self.name} 汪汪")                    # 读文件返回列表

d = Dog("旺财")                              repo = JsonNoteRepository("notes.json")
```

## 依赖注入 = 自己不造，外面传

```python
repo = JsonNoteRepository("notes.json")    # 先造仓库
service = NoteService(repo)                 # 把仓库传给服务（而不是服务自己造仓库）
```

**硬编码依赖：**
```python
class NoteService:
    def __init__(self):
        self.repository = JsonNoteRepository()  # 自己造 → 耦合死了
```

**依赖注入：**
```python
class NoteService:
    def __init__(self, repository: NoteRepository):
        self.repository = repository  # 外面传 → 可替换
```
