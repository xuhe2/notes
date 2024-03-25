使用PY实现



# 服务端



`import socket`导入包

`with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:`使用`with as`语句会在结束代码块的时候, 自动调用`.close`方法关闭

> - `socket.AF_INET` 表示 IPv4 地址家族
> - `socket.SOCK_STREAM` 表示流式套接字



```python
with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.bind(('0.0.0.0', 8888))
    s.listen()
```

* 注意, `bind`方法只能传入一个



```python
    with conn:
        print('Connected by', addr)
        while True:
            data = conn.recv(1024)
            if not data:
                break
            conn.sendall(data) #回传
```

接受处理数据



# 客户端

```python
import socket

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.connect(('localhost', 8888))
    s.sendall(b'Hello, world')
    data = s.recv(1024)
    print('Received', repr(data))
```

