# model预习(temp)

##       1.报错

```python
 Model class booktest.urls.BookInfo doesn't declare an explicit app_label and isn't in an application in INSTALLED_APPS. 
    
这一类报错一般是没注册子应用
有模型类是必须要注册子应用

```

##        2. 为什么用django创建完表后多出那么多表

![1589729454894](C:\Users\86155\AppData\Roaming\Typora\typora-user-images\1589729454894.png)

        ```python
因为 django 中有一个管理站点, 里面也定义了很多模型类
        ```



## 3.