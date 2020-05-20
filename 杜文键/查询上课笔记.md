## 查询

### get

模型类.objects.get(条件)
查询一个 若不存在抛出**模型类.DoesNotExist** 

### all

模型对象 .all() 



### filter

模型对象.filter(属性名__条件表达式=值)

如id范围(1,5) id__range(1,5)

### exclude

不等于



### F	

比较两个属性

```python
from django.db.models import F
BookInfo.objects.filter(bread__gte=F('bcomment'))
```



## 逻辑与

用 逗号 (bread__gt=20,id__lt=3)



## Q

逻辑或逻辑非

或: Q()|Q()

非: ~Q()



### 聚合

对象.aggregate()  sum avg count max min

返回一个字典

value = 字典对象.get('key') or value = 字典对象['key']



### 排序

对象.filter(条件).order_by(''字段'')  默认正序

​			.order_by(''-字段'')   降序





### 关联

#### 一查多

 一方对象.多方模型小写_set   +过滤或者查全部 filter(),all()

#### 多查一

多方对象.外键名    

#### 





## 日期

date(1991,01,01)=('1990-01-01')