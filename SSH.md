# `windows`安装使用

## 在设置里面安装

* 安装`OpenSSH`

  > 1. 客户端
  > 2. 服务器端



* 使用`ssh -v`检查是否成功安装



## 打开`计算机管理`

1. 在`左侧边栏`的`服务`中打开

2. 把启动类型改成`自动`

3. 回到`power shell`,使用

   ```shell
   Get-Service -Name *ssh*
   ```

   检查是否有两个运行中

4. 使用

   ```shell
   netstat -an | findstr :22
   ```

   ,检查是否正在监听22号端口

5. 使用

   ```shell
   ipconfig
   ```

   检查`IPV4 Address`的IP



## 连接

```shell
ssh [name]@ip
```



