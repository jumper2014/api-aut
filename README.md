# HTTP API Application Under Test
- 为了开发自动化测试框架，常常需要一个靶子，也就是待测应用。
- http-api-aut是一个非常简单的HTTP接口待测应用，实现了用户信息的增删改查，相当于Mock Server。
- 支持POST,GET,PUT,DELETE等基本HTTP请求方法。
- 请求体和响应体为application/json类型。
- 基于Python Flask开发。
- 使用简单，一键启动。

# 运行
- python main.py


# 数据结构
- 用户信息存储在MySQL数据库中，数据库名为"api"，表名为"user"
- 用户基本信息包含：用户ID，用户名，用户年龄

# 接口列表
- 4个接口用于用户管理
    - 用户创建: POST(非幂等操作)
    - 用户查询: GET
    - 用户更新: PUT(幂等操作，提供更新后的完整信息)
    - 用户删除: DELETE
## 接口使用
- 用户创建
```
curl -X POST \
  http://localhost:8080/user \
  -H 'Accept: application/json' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'Postman-Token: 8f52146e-2e9b-4287-9a73-430b85a7b9e2' \
  -d '{
  "name":"Python",
  "age":12

}'
```

- 用户查询
```
curl -X GET \
  http://localhost:8080/user/1 \
  -H 'Accept: application/json' \
  -H 'Cache-Control: no-cache' \
  -H 'Postman-Token: 23ebf87b-df79-47d5-9607-c990368c432c'
```

- 用户更新
```
curl -X PUT \
  http://localhost:8080/user/1 \
  -H 'Accept: application/json' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'Postman-Token: 81edae3e-c235-4e66-a52f-17fcc38a97ba' \
  -d '{
  "name":"python1",
  "age":20

}'
```

- 用户删除
```
curl -X DELETE \
  http://localhost:8080/user/1 \
  -H 'Accept: application/json' \
  -H 'Cache-Control: no-cache' \
  -H 'Postman-Token: c08ad01a-8592-4d2a-be7a-091476d5ffe8'
```

## 用户创建
###  请求格式
    POST /user
    Content-Type:application/json
    ACCEPT: application/json	
### 请求体
```json
{  
  "name": "python",
  "age": 24
}
```
### 请求参数含义
    name, string, 用户名
    age, int, 用户年龄
    userID, int, 用户唯一标识
### 响应格
    HTTP/1.1 status_code
    Content-Type:application/json
### 响应状态码
    200
### 响应body
```json
{  
    "userID": 1
}
```

## 用户查询
###  请求格式
    GET /user/{userID}
    ACCEPT: application/json	
### 请求体
    无
### 请求参数含义
    userID, int, 用户唯一标识, 必选
### 响应格
    HTTP/1.1 status_code
    Content-Type:application/json
### 响应状态码
    200
### 响应body
```json
{
  "userName": "python",
  "age": 24
}
``` 



## 用户信息更新
###  请求格式
    PUT /user/{userID}
    Content-Type:application/json
    ACCEPT: application/json	
### 请求体
```json
{  
  "name": "python",
  "age": 24
}
```
### 请求参数含义
    userID, int, 用户唯一标识, 必选
    name, string, 更新后的用户名
### 响应格
    HTTP/1.1 status_code
    Content-Type:application/json
### 响应状态码
    200
### 响应body
```json
{  
}
```

## 用户删除
###  请求格式
    DELETE /user/{userID}
    ACCEPT: application/json	
### 请求体
    无
### 请求参数含义
    userID, int, 用户唯一标识, 必选
### 响应格
    HTTP/1.1 status_code
    Content-Type:application/json
### 响应状态码
    200
### 响应body
```json
{  
}
```


