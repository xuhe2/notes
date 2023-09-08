> 使用`uvicorn main:app --reload`启动服务

> 使用`解包`操作使用把`dict`转换为一堆关键字传递



# 使用`pydantic`校验

```python
from pydantic import BaseModel


class User(BaseModel):
    id: int
    # 名字
    name: str
    # 年龄
    age: int


data_json = {
    'id': 1,
    'name': '张三',
    'age': 18
}

user = User(**data_json)
print(user)
```



* 可以转换为`dict`,`json`格式

> 使用`json`库



## 校验失败的时候

```python
from pydantic import ValidationError  # 验证错误
```



# 数据传输

1. 使用路径参数

```python
from typing import Optional

from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()  # 创建一个FastAPI类的实例


class CityInfo(BaseModel):
    # 检查新冠状病毒数据
    province: str
    country: str
    is_affected: Optional[bool]


# @app.get("/")
# def index():
#     return {"message": "Hello World"}


@app.get("/city/{city_name}")
def get_city_info(city_name: str):
    # 获取城市信息
    return CityInfo(province=city_name, country="中国", is_affected=True)
```



# 使用文档

> 文档内容是自动生产的

* 使用http://127.0.0.1:8000/docs检查



# 使用`uvicorn`模块

```python
uvicorn.run(app=app, host="127.0.0.1", port=8000, workers=1)
```



# 使用`APIRouter`

* 导入

```python
from fastapi import APIRouter
```

* 实例化

```python
router = APIRouter()
```

* 加入路由

```python
app.include_router(router, prefix="/router")
```

> 设置路由的`TAG`

```python
app.include_router(router, prefix="/router", tags=["router"])
```







# 限制传入的路径参数

```python
from fastapi import APIRouter, Path
number: int = Path(..., description="number", title="number", ge=1, le=100)
```



# 限制查询的参数

> 使用`Query`
>
> `from fastapi import Query`



# 使用`pydantic`还要校验的时候

> 使用`pydantic`的`Field`



# 当传递参数是一个`JSON`的时候

使用`pydantic`的`BaseModel`

* 使用内部类设置样例

```python
class CountryInfo(BaseModel):
    country: str
    people_number: int = Field(default=100, title="人口数量", description="国家的人口数量")

    class Config:
        schema_extra = {
            "example": {
                "country": "中国",
                "people_number": 14000,
            }
        }
```



# 设置`Cookie`和`Header`参数

* 检测的时候需要使用`postman`

> 需要`from fastapi import Cookie`使用



```python
@router.get("/header/")
def get_header(
        *,
        header: Optional[str] = Header(None, description="token", convert_underscores=True)
):
    return {"header": header}
```

> 使用`convert_underscores`转换下划线
>
> 比如`user_agent`变成`user-agent`.

```python
@router.get("/header/")
def get_header(
        user_agent: Optional[str] = Header(None, description="user agent"),
        x_token: Optional[str] = Header(None, description="token", convert_underscores=True)
):
    return {
        "user_agent": user_agent,
        "x_token": x_token
    }
```



# 响应模型

* 对于邮箱地址的检测可以使用`pydantic`的`EmailStr`

> 使用响应模型是因为不用返回不需要的部分



```python
class UserIn(BaseModel):
    username: str = Field(..., min_length=3, max_length=5)
    password: str = Field(..., min_length=6, max_length=12)
    email: str


class UserOut(BaseModel):
    username: str
    email: str
```

> 上述不需要返回密码



```python
@router.post("/users/", response_model=UserOut, status_code=201)
async def create_user(user: UserIn):
    return user
```



> 在修饰器中设置`response_model_exclude_defaults=True`,可以使默认值被忽略



> 设置需要返回的字段和不需要返回的字段
>
> 使用`response_model_include={"email"}`,`response_model_exclude={"email"}`



# 额外模型

- **输入模型**需要拥有密码属性。
- **输出模型**不应该包含密码。
- **数据库模型**很可能需要保存密码的哈希值。

```python
from fastapi import FastAPI
from pydantic import BaseModel, EmailStr

app = FastAPI()


class UserIn(BaseModel):
    username: str
    password: str
    email: EmailStr
    full_name: str | None = None


class UserOut(BaseModel):
    username: str
    email: EmailStr
    full_name: str | None = None


class UserInDB(BaseModel):
    username: str
    hashed_password: str
    email: EmailStr
    full_name: str | None = None


def fake_password_hasher(raw_password: str):
    return "supersecret" + raw_password


def fake_save_user(user_in: UserIn):
    hashed_password = fake_password_hasher(user_in.password)
    user_in_db = UserInDB(**user_in.dict(), hashed_password=hashed_password)
    print("User saved! ..not really")
    return user_in_db


@app.post("/user/", response_model=UserOut)
async def create_user(user_in: UserIn):
    user_saved = fake_save_user(user_in)
    return user_saved
```





# 响应状态码

> 需要导入`fastapi`的`status`模块

```python
@router.post("/status_code", status_code=status.HTTP_200_OK)
async def status_code():
    return {"status_code": 200}
```



