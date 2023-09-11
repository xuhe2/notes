* 考试带计算器

# 读文件

使用`read_*`的格式

比如,`read_csv`是读入`CSV`文件



* 对文件的时候设置开头记录的`index`

> 先设置`index_column_name`,比如`index_col="date.utc"`
>
> 再设置使用什么作为`index`的内容,比如`parse_dates=True`



# 写入文件

使用`to_*`的格式



# 常用方法

`info`: 查看信息

```python
In [10]: type(titanic[["Age", "Sex"]])
Out[10]: pandas.core.frame.DataFrame
```



# 查找

The returned data type is a pandas DataFrame:

```
In [10]: type(titanic[["Age", "Sex"]])
Out[10]: pandas.core.frame.DataFrame
```



```python
above_35 = titanic[titanic["Age"] > 35]
```

> 上述返回的是一个矩阵,内容是`True`,`False`



# 查找存在数值的

The [`notna()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.notna.html#pandas.Series.notna) conditional function returns a `True` for each row the values are not a `Null` value. As such, this can be combined with the selection brackets `[]` to filter the data table.



# 添加新的列

> 直接使用新的`key`会直接创建新的列

```
air_quality["ratio_paris_antwerp"] = (
   ...:     air_quality["station_paris"] / air_quality["station_antwerp"]
```



# 修改新的列

> 使用`rename`修改列的名字



# 数字处理

* 求平均值

```
titanic["Age"].mean()
```



* 求中位数

```
titanic[["Age", "Fare"]].median()
```



* 求各种数值总结的形容

```
titanic[["Age", "Fare"]].describe()
```



# 合并数据表

> 使用`concat`方法

```
air_quality = pd.concat([air_quality_pm25, air_quality_no2], axis=0)
```

> `axis`参数代表你合并的是哪个坐标轴
>
> `0`代表你合并的是行的内容
>
> `1`代表合并的列的内容



# 根据数值进行排序

> 使用`sort_values`方法

```python
print(file1.sort_values("money"))
```

