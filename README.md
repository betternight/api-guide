> 好的接口规范能约束开发人员，能降低前后端人员之间的沟通协调，能避免后期联调带来的一系列问题。

## 协议
1. http

2. https ( 数据的传输安全 )

## 域名
应该尽量将API部署在专用域名之下， 如果确定API很简单，不会有进一步扩展，可以考虑放在主域名下

## API 版本控制
1. 将API的版本号放入URL：http://{ url}/v{n}/

2. 将版本号放在HTTP头信息中

3. 版本号,分为整形和浮点型。

- 整形的版本号: 大功能版本发布形式；具有当前版本状态下的所有API接口 ,例如：v1,v2

- 浮点型：为小版本号，只具备补充api的功能，其他api都默认调用对应大版本号的api 例如：v1.1 v2.2

## API 路径规则
```html
路径又称"终点"（endpoint），表示API的具体网址。

在RESTful架构中，每个网址代表一种资源（resource），所以网址中不能有动词，只能有名词，
而且所用的名词往往与数据库的表格名对应。一般来说，数据库中的表都是同种记> > 录的"集合"（collection），所以API中的名词也应该使用复数。
```

举例来说，有一个API提供动物园（zoo）的信息，还包括各种动物和雇员的信息，则它的路径应该设计成下面这样。

```html
https://api.{url}.com/v1/products

https://api.{url}.com/v1/users

https://api.{url}.com/v1/employees
```

## HTTP请求方式
```html
对于资源的具体操作类型，由HTTP动词表示。

常用的HTTP动词有下面四个（括号里是对应的SQL命令）。
```

- GET（SELECT） ：从服务器取出资源（一项或多项）。

- POST （CREATE） ：在服务器新建一个资源。

- PUT （UPDATE） ： 在服务器更新资源（客户端提供改变后的完整资源）。

- DELETE （DELETE） ：从服务器删除资源。

### 下面是一些例子
- GET /product：列出所有商品

- POST /product：新建一个商品

- GET /product/ID：获取某个指定商品的信息

- PUT /product/ID：更新某个指定商品的信息

- DELETE /product/ID：删除某个商品

- GET /product/ID/purchase ：列出某个指定商品的所有投资者

- GET /product/ID/purchase/ID：获取某个指定商品的指定投资者信息

## 过滤信息
如果记录数量很多，服务器不可能都将它们返回给用户。API应该提供参数，过滤返回结果。

下面是一些常见的参数。

- ?limit=10：指定返回记录的数量

- ?offset=10：指定返回记录的开始位置。

- ?page=2&per_page=100：指定第几页，以及每页的记录数。

- ?sortby=name&order=asc：指定返回结果按照哪个属性排序，以及排序顺序。

- ?producy_type=1：指定筛选条件

## API 传入参数
- * RESTful 地址栏参数 /api/v1/product/122 122为产品编号，获取产品为122的信息

- * GET方式的查询字串 见过滤信息小节

- 请求Body数据

- Cookie，Request Header 。注：Cookie和Header 一般都是用于OAuth认证的2种途径

### 返回数据
只要api接口成功接到请求，就不能返回200以外的HTTP状态。

为了保障前后端的数据交互的顺畅，建议规范数据的返回，并采用固定的数据格式封装。

```html
//  接口返回模板： 
{

    code: 200,

    data: {} || [],

    msg: '说明信息'

}
```
- code: 接口的执行的状态 = 200 表示成功，其它表示有异常

- data 接口的主要数据，可以根据时间返回数据或对象

- msg 当前 Status ！= 200 都应该有错误描述信息
