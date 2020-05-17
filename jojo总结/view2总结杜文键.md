# view总结之请求，响应，路由转换，重定向

### 常见错误

405 一般是请求方法错误

500 错误提示 line 1 column 1 一般是解释请求体数据 格式错误

### Http请求

​	根据客户端发的请求，后端得到想要的数据

1. #### 查询字符串参数

   ```bash
   无论客户端以什么方式请求，如post，get,提取字符串参数都是用request.GET ---此处request代表封装后的请求对象参数
   ```

   

####             2.请求体数据

- 表单类型

  ```bash
  body=request.POST  ---QueryDict对象
  body.get('xx') 取出值
  ```

  

- #### 非表单类型	     

  ```bash
  90%是json类型
  import json
  
  json_str = request.body --byte类型数据
  json.loads(json_str) --转换成字典
  再用 .get 取值
  
  ```


- ####         请求头

​		              request.META

###         路由转换器  --请求路径参数用到

####          注意

- ​	  通过正则限制参数类型
- ​          作用提高代码复用性
- ​           默认位置  from django.urls import register_converter # 默认路由转换器地址
- ​	   视图内部关键字参数必须和路由中关键字一样



####    步骤

1. ​    在项目任何可以导入模块的路径新建一个python文件  如 converters.py,然后复制默认路由器的样本，再改名字，改正则，达到自己想要效果

   

    ```bash
class MobileConverter:

  regex = '1[3-9]\d{9}'

  def to_python(self, value):
     
      return int(value)

  def to_url(self, value):
     
      return str(value)
    ```

​         2.根目录urls.py 注册总路由  

        ```bash
from django.urls import register_converter

from 自己新建py文件 import 自己定义路由转换器的类:如下
from .converters import MobileConverter

        ```



​          3.根据自己定义的正则注册子路由



### Http响应

- HTTPResponse(): 响应多种数据类型

  ```python
  def __init__(self, content=b'', *args, **kwargs):
      pass
  
  HttpResponse(content='')
  可以忽略content=
  还有 content_type=响应体数据类型，默认为text/html, status=状态码，默认为200
  
  ```

  

- json 响应

  ```python
  def __init__(self, data, encoder=DjangoJSONEncoder, safe=True,
                   json_dumps_params=None, **kwargs):
      
  默认传入 data参数格式是字典， safe=False则可以传入列表
  准备 字典 data={
      xxx
  }
  
  返回 return JsonResponse(data)--转换成json数据
  ```



###      重定向



return redirect('重定向地址')

注意：重定向的路径前没加    /   （#根路径） HTTP协议默认当成拼接请求路径和重定向路径 如       login/        重定向      return redirect('index/')   ---->跳转到 login/index/      所以要写成 redirect('/index/')





#### 问题:如果主页也是重定向，会不会死循环呀 ====》

需要了解死循环的条件的是什么？就是相互依赖或者调用。但是重定向只是http封装的的操作，跟调用和依赖没有任何的关系 

每个请求，如果响应后，网络的状态就断掉了

​	