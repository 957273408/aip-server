# api
- 基准路径：http://127.0.0.1:8888/api/private/v1/

> 除了登录接口，其他所有接口请求头必须设置为Authorization=token (token为登录成功后服务器返回的认证token)

## 登录
### 登录验证接口
- 请求路径：login
- 请求方法：post
- 请求参数

| 参数名      | 参数说明 | 备注   |
| -------- | ---- | ---- |
| username | 用户名  | 不能为空 |
| password | 密码   | 不能为空 |

- 响应参数

| 参数名      | 参数说明   | 备注       |
| -------- | ------ | -------- |
| id       | 用户ID   |          |
| rid      | 用户角色ID |          |
| username | 用户名    |          |
| mobile   | 手机号    |          |
| email    | 邮箱     |          |
| token    | 令牌     | 基于jwt的令牌 |
- 响应数据
```javascript
{
    "data": {
        "id": 500,
        "rid": 0,
        "username": "admin",
        "mobile": "123",
        "email": "123@qq.com",
        "token": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOjUwMCwicmlkIjowLCJpYXQiOjE1MTI1NDQyOTksImV4cCI6MTUxMjYzMDY5OX0.eGrsrvwHm-tPsO9r_pxHIQ5i5L1kX9RX444uwnRGaIM"
    },
    "meta": {
        "msg": "登录成功",
        "status": 200
    }
}
```

## 用户管理

### 用户数据列表
- 请求路径：users
- 请求方法：get
- 请求参数

| 参数名      | 参数说明   | 备注   |
| -------- | ------ | ---- |
| query    | 查询参数   | 可以为空 |
| pagenum  | 当前页码   | 不能为空 |
| pagesize | 每页显示条数 | 不能为空 |

- 响应参数

| 参数名       | 参数说明   | 备注   |
| --------- | ------ | ---- |
| totalpage | 总记录数   |      |
| pagenum   | 当前页码   |      |
| users     | 用户数据集合 |      |

- 响应数据
```javascript
{
    "data": {
        "totalpage": 5,
        "pagenum": 4,
        "users": [
            {
                "id": 25,
                "username": "tige117",
                "mobile": "18616358651",
                "type": 1,
                "openid": "",
                "email": "tige112@163.com",
                "create_time": "2017-11-09T20:36:26.000Z",
                "modify_time": null,
                "is_delete": false,
                "is_active": false
            }
        ]
    },
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

### 添加用户
- 请求路径：users
- 请求方法：post
- 请求参数

| 参数名      | 参数说明 | 备注   |
| -------- | ---- | ---- |
| username | 用户名称 | 不能为空 |
| password | 用户密码 | 不能为空 |
| email    | 邮箱   | 可以为空 |
| mobile   | 手机号  | 可以为空 |

- 响应参数

| 参数名      | 参数说明   | 备注   |
| -------- | ------ | ---- |
| id       | 用户ID   |      |
| rid      | 用户角色ID |      |
| username | 用户名    |      |
| mobile   | 手机号    |      |
| email    | 邮箱     |      |

- 响应数据
```javascript
{
    "data": {
        "id": 28,
        "username": "tige1200",
        "mobile": "test",
        "type": 1,
        "openid": "",
        "email": "test@test.com",
        "create_time": "2017-11-10T03:47:13.533Z",
        "modify_time": null,
        "is_delete": false,
        "is_active": false
    },
    "meta": {
        "msg": "用户创建成功",
        "status": 201
    }
}
```

### 修改用户状态
- 请求路径：users/:uId/state/:type
- 请求方法：put
- 请求参数

| 参数名  | 参数说明 | 备注            |
| ---- | ---- | ------------- |
| uId   | 用户ID | 不能为空`携带在url中` |
| type   | 用户状态 | 不能为空`携带在url中`，值为true或者false|

- 响应数据 
```javascript
{
  "data": {
    "id": 566,
    "rid": 30,
    "username": "admin",
    "mobile": "123456",
    "email": "bb@itcast.com",
    "mg_state": 0
  },
  "meta": {
    "msg": "设置状态成功",
    "status": 200
  }
}
```

### 根据ID查询用户信息
- 请求路径：users/:id
- 请求方法：get
- 请求参数

| 参数名  | 参数说明 | 备注            |
| ---- | ---- | ------------- |
| id   | 用户ID | 不能为空`携带在url中` |

- 响应参数

| 参数名   | 参数说明 | 备注 |
| :------- | -------- | ---- |
| id       | 用户ID   |      |
| username | 用户名   |      |
| role_id  | 角色ID   |      |
| mobile   | 手机号   |      |
| email    | 邮箱     |      |

- 响应数据
```javascript
{
    "data": {
        "id": 503,
        "username": "admin3",
        "password": "123456"
        "role_id": 0,
        "mobile": "00000",
        "email": "new@new.com"
    },
    "meta": {
        "msg": "更新成功",
        "status": 200
    }
}
```

### 编辑用户提交
- 请求路径：users/:id
- 请求方法：put
- 请求参数

| 参数名 | 参数说明 | 备注                        |
| ------ | -------- | --------------------------- |
| id     | 用户id   | 不能为空 `参数是url参数:id` |
| email  | 邮箱     | 可以为空,放在请求体中       |
| mobile | 手机号   | 可以为空,放在请求体中       |

- 响应参数

| 参数名     | 参数说明 | 备注   |
| ------- | ---- | ---- |
| id      | 用户ID |      |
| role_id | 角色ID |      |
| mobile  | 手机号  |      |
| email   | 邮箱   |      |

- 响应数据
```javascript
/* 200表示成功，500表示失败 */
{
    "data": {
        "id": 503,
        "username": "admin3",
        "role_id": 0,
        "mobile": "111",
        "email": "123@123.com"
    },
    "meta": {
        "msg": "更新成功",
        "status": 200
    }
}
```
### 删除单个用户
- 请求路径：users/:id
- 请求方法：delete
- 请求参数

| 参数名  | 参数说明 | 备注                |
| ---- | ---- | ----------------- |
| id   | 用户id | 不能为空`参数是url参数:id` |

- 响应参数

- 响应数据
```javascript
{
    "data": null,
    "meta": {
        "msg": "删除成功",
        "status": 200
    }
}
```

### 给用户分配角色
- 请求路径：users/:id/role
- 请求方法：put
- 请求参数

| 参数名  | 参数说明 | 备注                |
| ---- | ---- | ----------------- |
| id   | 用户ID | 不能为空`参数是url参数:id` |
| rid  | 角色id | 不能为空`参数body参数`    |

- 响应参数

| 参数名     | 参数说明 | 备注   |
| ------- | ---- | ---- |
| id      | 用户ID |      |
| role_id | 角色ID |      |
| mobile  | 手机号  |      |
| email   | 邮箱   |      |

- 响应数据
```javascript
{
    "data": {
        "id": 508,
        "rid": "30",
        "username": "asdf1",
        "mobile": "123123",
        "email": "adfsa@qq.com"
    },
    "meta": {
        "msg": "设置角色成功",
        "status": 200
    }
}
```
## 权限管理
### 所有权限列表
- 请求路径：rights/:type
- 请求方法：get
- 请求参数

| 参数名  | 参数说明 | 备注                                       |
| ---- | ---- | ---------------------------------------- |
| type | 类型   | 值: list 或 tree , list 列表显示权限, tree 树状显示权限,`参数是url参数:type` |

- 响应参数

| 参数名   | 参数说明     | 备注                                |
| -------- | ------------ | ----------------------------------- |
| id       | 权限ID       |                                     |
| authName | 权限说明     |                                     |
| level    | 权限层级     | 0:一级权限  1:二级权限   2:三级权限 |
| pid      | 权限父ID     |                                     |
| path     | 对应访问路径 |                                     |


- 响应数据
  type=list
```javascript
	{
    "data": [
        {
            "id": 101,
            "authName": "商品管理",
            "level": "0",
            "pid": 0,
            "path": "goods"
        },
        {
            "id": 102,
            "authName": "订单管理",
            "level": "0",
            "pid": 0,
            "path": "orders"
        }
    ],
    "meta": {
        "msg": "获取权限列表成功",
        "status": 200
    }
}
```
type=tree
```javascript
[
    {
    "data": [
        {
            "id": 101,
            "authName": "商品管理",
            "path": null,
            "pid": 0,
            "children": [
                {
                    "id": 104,
                    "authName": "商品列表",
                    "path": null,
                    "pid": 101,
                    "children": [
                        {
                            "id": 105,
                            "authName": "添加商品",
                            "path": null,
                            "pid": "104,101"
                        }
                    ]
                }
            ]
        }
    ],
    "meta": {
        "msg": "获取权限列表成功",
        "status": 200
    }
}
]
```

### 左侧菜单权限
- 请求路径：menus
- 请求方法：get
- 响应数据

```javascript
{
    "data": [
        {
            "id": 101,
            "authName": "商品管理",
            "path": null,
            "children": [
                {
                    "id": 104,
                    "authName": "商品列表",
                    "path": "/goodslist",
                    "children": []
                }
            ]
        }
    "meta": {
        "msg": "获取菜单列表成功",
        "status": 200
    }
}
```

## 角色管理
### 角色列表
- 请求路径：roles
- 请求方法：get
- 响应数据说明
  - 第一层为角色信息
  - 第二层开始为权限说明，权限一共有3层权限
- 响应数据
```javascript
{
    "data": [
        {
            "id": 30,
            "roleName": "主管",
            "roleDesc": "技术负责人",
            "children": [
                {
                    "id": 101,
                    "authName": "商品管理",
                    "path": null,
                    "children": [
                        {
                            "id": 104,
                            "authName": "商品列表",
                            "path": null,
                            "children": [
                                {
                                    "id": 105,
                                    "authName": "添加商品",
                                    "path": null
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    ],
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```
### 添加角色
- 请求路径：roles
- 请求方法：post
- 请求参数

| 参数名      | 参数说明 | 备注   |
| -------- | ---- | ---- |
| roleName | 角色名称 | 不能为空 |
| roleDesc | 角色描述 | 可以为空 |

- 响应参数

| 参数名      | 参数说明 | 备注   |
| -------- | ---- | ---- |
| roleId   | 角色ID |      |
| roleName | 角色名称 |      |
| roleDesc | 角色描述 |      |

- 响应数据

```javascript
{
    "data": {
        "roleId": 40,
        "roleName": "admin2",
        "roleDesc": "admin2Desc"
    },
    "meta": {
        "msg": "创建成功",
        "status": 201
    }
}
```

### 根据ID查询角色
- 请求路径：roles/:id
- 请求方法：get
- 请求参数

| 参数名  | 参数说明 | 备注            |
| ---- | ---- | ------------- |
| :id  | 角色ID | 不能为空`携带在url中` |

- 响应参数

| 参数名      | 参数说明 | 备注   |
| -------- | ---- | ---- |
| roleId   | 角色ID |      |
| roleName | 角色名称 |      |
| roleDesc | 角色描述 |      |

- 响应数据
```javascript
{
    "data": {
        "roleId": 31,
        "roleName": "测试角色",
        "roleDesc": "测试负责人"
    },
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

### 编辑提交角色
- 请求路径：roles/:id
- 请求方法：put
- 请求参数

| 参数名      | 参数说明 | 备注            |
| -------- | ---- | ------------- |
| :id      | 角色ID | 不能为空`携带在url中` |
| roleName | 角色名称 | 不能为空          |
| roleDesc | 角色描述 | 可以为空          |

- 响应数据

```javascript
{
    "data": {
        "roleId": 31,
        "roleName": "测试角色",
        "roleDesc": "测试角色描述"
    },
    "meta": {
        "msg": "修改成功",
        "status": 200
    }
}
```
### 删除角色
- 请求路径：roles/:id
- 请求方法：delete
- 请求参数

| 参数名  | 参数说明 | 备注            |
| ---- | ---- | ------------- |
| :id  | 角色ID | 不能为空`携带在url中` |

- 响应数据

```javascript
{
    "data": null,
    "meta": {
        "msg": "删除成功",
        "status": 200
    }
}
```

### 角色授权
- 请求路径：roles/:roleId/rights
- 请求方法：post
- 请求参数

| 参数名  | 参数说明   | 备注              |
| ---- | ------ | --------------- |
| :roleId  | 角色ID   | 不能为空`携带在url中`   |
| rids | 权限ID列表 | 以 `,` 分割的权限ID列表，放在请求体中，<br />注意：每个权限id的父级id必须带过去，直到顶层节点id |

- 响应数据

```javascript
{
    "data": null,
    "meta": {
        "msg": "更新成功",
        "status": 200
    }
}
```

### 删除角色指定权限
- 请求路径：roles/:roleId/rights/:rightId
- 请求方法：delete
- 请求参数

| 参数名      | 参数说明 | 备注            |
| -------- | ---- | ------------- |
| :roleId  | 角色ID | 不能为空`携带在url中` |
| :rightId | 权限ID | 不能为空`携带在url中` |

- 响应数据说明
  - 返回当前所有拥有的角色信息 
- 响应数据
```javascript
{
    "data": [
        {
            "id": 101,
            "authName": "商品管理",
            "path": null,
            "children": [
                {
                    "id": 104,
                    "authName": "商品列表",
                    "path": null,
                    "children": [
                        {
                            "id": 105,
                            "authName": "添加商品",
                            "path": null
                        },
                        {
                            "id": 116,
                            "authName": "修改",
                            "path": null
                        }
                    ]
                }
            ]
        }
    ],
    "meta": {
        "msg": "取消权限成功",
        "status": 200
    }
}
```
## 商品分类管理
### 商品分类数据列表
- 请求路径：categories
- 请求方法：get
- 请求参数

| 参数名   | 参数说明 | 备注                                                         |
| -------- | -------- | ------------------------------------------------------------ |
| type     | [1,2,3]  | 值：1，2，3分别表示显示一层二层三层分类列表，写3代表三个级别的分类都获取  必须 |
| pagenum  | 页码     | 可选                                                         |
| pagesize | 页容量   | 可选                                                         |

- 响应参数

| 参数名       | 参数说明   | 备注   |
| --------- | ------ | ---- |
| cat_id    | 分类ID   |      |
| cat_name  | 分类名称   |      |
| cat_pid   | 分类父ID  |      |
| cat_level | 分类当前层级 |      |

- 响应数据
```javascript
{
    "data": [
        {
            "cat_id": 1,
            "cat_name": "手机相机",
            "cat_pid": 0,
            "cat_level": 0
        },
        {
            "cat_id": 2,
            "cat_name": "电脑办公",
            "cat_pid": 0,
            "cat_level": 0
        }
    ],
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

### 添加分类
- 请求路径：categories
- 请求方法：post
- 请求参数

| 参数名    | 参数说明               | 备注     |
| --------- | ---------------------- | -------- |
| cat_pid   | 分类父ID               | 不能为空 |
| cat_name  | 分类名称               | 不能为空 |
| cat_level | 分类层级，不能超过三级 | 不能为空 |

- 响应数据

```javascript
{
    "data": {
        "cat_id": 62,
        "cat_name": "相框",
        "cat_pid": "1",
        "cat_level": "1"
    },
    "meta": {
        "msg": "创建成功",
        "status": 201
    }
}
```

### 根据id查询分类
- 请求路径：categories/:id
- 请求方法：get
- 请求参数

| 参数名  | 参数说明 | 备注            |
| ---- | ---- | ------------- |
| :id  | 分类ID | 不能为空`携带在url中` |

- 响应数据

```javascript
{
    "data": {
        "cat_id": 3,
        "cat_name": "厨卫电器",
        "cat_pid": 0,
        "cat_level": 0
    },
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

### 编辑提交分类
- 请求路径：categories/:id
- 请求方法：put
- 请求参数

| 参数名      | 参数说明 | 备注            |
| -------- | ---- | ------------- |
| :id      | 分类ID | 不能为空`携带在url中` |
| cat_name | 分类名称 | 不能为空          |

- 响应数据

```javascript
{
    "data": {
        "cat_id": 22,
        "cat_name": "自拍杆",
        "cat_pid": 7,
        "cat_level": 2
    },
    "meta": {
        "msg": "更新成功",
        "status": 200
    }
}
```

### 删除分类
- 请求路径：categories/:id
- 请求方法：delete
- 请求参数

| 参数名  | 参数说明 | 备注            |
| ---- | ---- | ------------- |
| :id  | 分类ID | 不能为空`携带在url中` |

- 响应数据

```javascript
{
    "data": null,
    "meta": {
        "msg": "删除成功",
        "status": 200
    }
}
```

## 分类参数管理
### 参数列表
- 请求路径：categories/:id/attributes
- 请求方法：get
- 请求参数

| 参数名 | 参数说明    | 备注                                                  |
| ------ | ----------- | ----------------------------------------------------- |
| :id    | 分类ID      | 不能为空，必须是三级ID`携带在url中`                   |
| sel    | [only,many] | 不能为空,通过only或many来获取分类静态参数还是动态参数 |

- 响应参数

| 参数名        | 参数说明                            | 备注   |
| ---------- | ------------------------------- | ---- |
| attr_id    | 分类参数ID                          |      |
| attr_name  | 分类参数名称                          |      |
| cat_id     | 分类参数所属分类                        |      |
| attr_sel   | only:输入框(唯一)  many:后台下拉列表/前台单选框 |      |
| attr_write | manual:手工录入  list:从列表选择         |      |
| attr_vals  | 如果attr_write:list,那么有值，该值以逗号分隔  |      |

- 响应数据

```javascript
{
    "data": [
        {
            "attr_id": 1,
            "attr_name": "cpu",
            "cat_id": 22,
            "attr_sel": "only",
            "attr_write": "manual",
            "attr_vals": "ffff"
        }
    ],
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

### 添加参数
- 请求路径：categories/:id/attributes
- 请求方法：post
- 请求参数

| 参数名    | 参数说明    | 备注                           |
| --------- | ----------- | ------------------------------ |
| :id       | 分类ID      | 不能为空`携带在url中`          |
| attr_name | 参数名称    | 不能为空                       |
| attr_sel  | [only,many] | 不能为空                       |
| attr_vals | 参数值      | 动态参数时可选，静态属性时必填 |

- 响应数据

```javascript
{
    "data": {
        "attr_id": 44,
        "attr_name": "测试参数",
        "cat_id": "1",
        "attr_sel": "many",
        "attr_write": "list",
        "attr_vals": "a,b,c"
    },
    "meta": {
        "msg": "创建成功",
        "status": 201
    }
}
```
### 修改参数
- 请求路径：categories/:id/attributes/:attrid
- 请求方法：put
- 请求参数

| 参数名    | 参数说明    | 备注                           |
| --------- | ----------- | ------------------------------ |
| :id       | 分类ID      | 不能为空`携带在url中`          |
| :attrid   | 参数ID      | 不能为空`携带在url中`          |
| attr_name | 参数名称    | 不能为空                       |
| attr_sel  | [only,many] | 不能为空                       |
| attr_vals | 参数值      | 动态参数时可选，静态属性时必填 |

- 响应数据

```javascript
{
    "data": [
        {
            "attr_id": 1,
            "attr_name": "cpu",
            "cat_id": 22,
            "attr_sel": "only",
            "attr_write": "manual",
            "attr_vals": "ffff"
        }
    ],
    "meta": {
        "msg": "更新成功",
        "status": 200
    }
}
```

### 删除参数
- 请求路径：categories/:id/attributes/:attrid
- 请求方法：delete
- 请求参数

| 参数名     | 参数说明 | 备注            |
| ------- | ---- | ------------- |
| :id     | 分类ID | 不能为空`携带在url中` |
| :attrid | 参数ID | 不能为空`携带在url中` |

- 响应数据

```javascript
{
    "data": null,
    "meta": {
        "msg": "删除成功",
        "status": 200
    }
}
```

### 根据ID查询参数
- 请求路径：categories/:id/attributes/:attrId
- 请求方法：get
- 请求参数

| 参数名   | 参数说明    | 备注                  |
| -------- | ----------- | --------------------- |
| :id      | 分类ID      | 不能为空`携带在url中` |
| :attrId  | 属性ID      | 不能为空`携带在url中` |
| attr_sel | [only,many] | 不能为空              |

- 响应数据

```javascript
{
    "data": {
        "attr_id": 1,
        "attr_name": "cpu",
        "cat_id": 22,
        "attr_sel": "only",
        "attr_write": "manual",
        "attr_vals": "ffff"
    },
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

### 添加/删除动态参数属性
- 请求路径：categories/:id/attributes/:attrId
- 请求方法：put
- 请求参数

| 参数名    | 参数说明 | 备注                     |
| --------- | -------- | ------------------------ |
| :id       | 分类ID   | 不能为空`携带在url中`    |
| :attrId   | 属性ID   | 不能为空`携带在url中`    |
| attr_name | 属性名称 | 不能空                   |
| attr_sel  | many     | 动态参数                 |
| attr_vals | 动态参数 | 多个参数值之间以逗号分割 |

- 响应数据

```javascript
{
    "data": {
        "attr_id": 9,
        "attr_name": "测试更新",
        "cat_id": "43",
        "attr_sel": "only",
        "attr_write": "manual",
        "attr_vals": "abc"
    },
    "meta": {
        "msg": "更新成功",
        "status": 200
    }
}
```

## 商品管理
### 商品列表数据
- 请求路径：goods
- 请求方法：get
- 请求参数

| 参数名      | 参数说明   | 备注   |
| -------- | ------ | ---- |
| query    | 查询参数   | 可以为空 |
| pagenum  | 当前页码   | 不能为空 |
| pagesize | 每页显示条数 | 不能为空 |

- 响应参数

| 参数名          | 参数说明   | 备注                        |
| ------------ | ------ | ------------------------- |
| total        | 总共商品条数 |                           |
| pagenum      | 当前商品页数 |                           |
| goods_id     | 商品ID   |                           |
| goods_name   | 商品名称   |                           |
| goods_price  | 价格     |                           |
| goods_number | 数量     |                           |
| goods_weight | 重量     | 不能为空                      |
| goods_state  | 商品状态   | 商品状态 0: 未通过 1: 审核中 2: 已审核 |
| add_time     | 添加时间   |                           |
| upd_time     | 更新时间   |                           |
| hot_mumber   | 热销品数量  |                           |
| is_promote   | 是否是热销品 |                           |

- 响应数据

```javascript
{
    "data": {
        "total": 50,
        "pagenum": "1",
        "goods": [
            {
                "goods_id": 144,
                "goods_name": "asfdsd",
                "goods_price": 1,
                "goods_number": 1,
                "goods_weight": 1,
                "goods_state": null,
                "add_time": 1512954923,
                "upd_time": 1512954923,
                "hot_mumber": 0,
                "is_promote": false
            }
        ]
    },
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

### 添加商品
- 请求路径：goods
- 请求方法：post
- 请求参数

| 参数名             | 参数说明          | 备注   |
| --------------- | ------------- | ---- |
| goods_name      | 商品名称          | 不能为空 |
| goods_cat     | 以为','分割的分类列表            | 不能为空 |
| goods_price     | 价格            | 不能为空 |
| goods_number    | 数量            | 不能为空 |
| is_promote | 是否促销 | 可以为空 |
| goods_introduce | 介绍            | 可以为空 |
| pics            | 上传的图片临时路径（数组） | 可以为空 |
| attrs           | 商品的参数（数组）     | 可以为空 |


- 请求数据

```javascript
{
	"goods_name":"test_goods_name2",
	"goods_price":20,
	"goods_number":30,
	"goods_weight":40,
	"goods_introduce":"abc",
	"pics":[
		{"pic":"/tmp_uploads/30f08d52c551ecb447277eae232304b8"}
		],
	"attrs":[
		{
			"attr_id":15,
			"attr_value":"ddd"
		},
		{
			"attr_id":15,
			"attr_value":"eee"
		}
		]
}
```


- 响应参数

| 参数名          | 参数说明          | 备注                                       |
| ------------ | ------------- | ---------------------------------------- |
| total        | 总共商品条数        |                                          |
| pagenum      | 当前商品页数        |                                          |
| goods_id     | 商品ID          |                                          |
| goods_cat     | 以为','分割的分类列表            |  |
| goods_name   | 商品名称          |                                          |
| goods_price  | 价格            |                                          |
| goods_number | 数量            |                                          |
| goods_weight | 重量            | 不能为空                                     |
| goods_state  | 商品状态          | 商品状态 0: 未通过 1: 审核中 2: 已审核                |
| add_time     | 添加时间          |                                          |
| upd_time     | 更新时间          |                                          |
| hot_mumber   | 热销品数量         |                                          |
| is_promote   | 是否是热销品        |                                          |
| pics         | 上传的图片临时路径（对象） | pics_id:图片ID,goods_id:商品ID,pics_big:大图,pics_mid:中图,pics_sma:小图 |
| attrs        | 商品的参数（数组）     | goods_id:商品ID,attr_value:当前商品的参数值,add_price:浮动价格,attr_vals:预定义的参数值,attr_sel:手动输入，还是单选, |

- 响应数据

```javascript
{
    "data": {
        "goods_id": 145,
        "goods_name": "test_goods_name2",
        "goods_price": 20,
        "cat_id": 1,
        "goods_number": 30,
        "goods_weight": 40,
        "goods_introduce": "abc",
        "goods_big_logo": "",
        "goods_small_logo": "",
        "goods_state": 1,
        "add_time": 1512962370,
        "upd_time": 1512962370,
        "hot_mumber": 0,
        "is_promote": false,
        "pics": [
            {
                "pics_id": 397,
                "goods_id": 145,
                "pics_big": "uploads/goodspics/big_30f08d52c551ecb447277eae232304b8",
                "pics_mid": "uploads/goodspics/mid_30f08d52c551ecb447277eae232304b8",
                "pics_sma": "uploads/goodspics/sma_30f08d52c551ecb447277eae232304b8"
            }
        ],
        "attrs": [
            {
                "goods_id": 145,
                "attr_id": 15,
                "attr_value": "ddd",
                "add_price": null,
                "attr_name": "fffffff",
                "attr_sel": "many",
                "attr_write": "list",
                "attr_vals": ""
            },
            {
                "goods_id": 145,
                "attr_id": 15,
                "attr_value": "eee",
                "add_price": null,
                "attr_name": "fffffff",
                "attr_sel": "many",
                "attr_write": "list",
                "attr_vals": ""
            }
        ]
    },
    "meta": {
        "msg": "创建商品成功",
        "status": 201
    }
}
```

### 根据ID查询商品
- 请求路径：goods/:id
- 请求方法：get
- 请求参数

| 参数名  | 参数说明 | 备注            |
| ---- | ---- | ------------- |
| id   | 商品ID | 不能为空`携带在url中` |

- 响应参数

| 参数名       | 参数说明                   | 备注                                                         |
| ------------ | -------------------------- | ------------------------------------------------------------ |
| goods_id     | 商品ID                     |                                                              |
| cat_id       | 分类Id                     |                                                              |
| cat_one_id   | 一级分类Id                 |                                                              |
| cat_two_id   | 二级分类Id                 |                                                              |
| cat_three_id | 三级分类Id                 |                                                              |
| goods_cat    | 商品三级分类组成的字符串   | 例如:"1,3,6"                                                 |
| goods_name   | 商品名称                   |                                                              |
| goods_price  | 价格                       |                                                              |
| goods_number | 数量                       |                                                              |
| goods_weight | 重量                       | 不能为空                                                     |
| goods_state  | 商品状态                   | 商品状态 0: 未通过 1: 审核中 2: 已审核                       |
| add_time     | 添加时间                   |                                                              |
| upd_time     | 更新时间                   |                                                              |
| hot_mumber   | 热销品数量                 |                                                              |
| is_promote   | 是否是热销品               |                                                              |
| pics         | 上传的图片临时路径（对象） | pics_id:图片ID,goods_id:商品ID,pics_big:大图,pics_mid:中图,pics_sma:小图 |
| attrs        | 商品的参数（数组）         | goods_id:商品ID,attr_value:当前商品的参数值,add_price:浮动价格,attr_vals:预定义的参数值,attr_sel:手动输入，还是单选, |

- 响应数据

```javascript
{
    "data": {
        "goods_id": 145,
        "cat_id": 6
		"cat_one_id": 1
		"cat_three_id": 6
		"cat_two_id": 3
        "goods_cat": "1,3,6"
        "goods_name": "test_goods_name2",
        "goods_price": 20,
        "goods_number": 30,
        "goods_weight": 40,
        "goods_introduce": "abc",
        "goods_big_logo": "",
        "goods_small_logo": "",
        "goods_state": 1,
        "add_time": 1512962370,
        "upd_time": 1512962370,
        "hot_mumber": 0,
        "is_promote": false,
        "pics": [
            {
                "pics_id": 397,
                "goods_id": 145,
                "pics_big": "uploads/goodspics/big_30f08d52c551ecb447277eae232304b8",
                "pics_mid": "uploads/goodspics/mid_30f08d52c551ecb447277eae232304b8",
                "pics_sma": "uploads/goodspics/sma_30f08d52c551ecb447277eae232304b8"
            }
        ],
        "attrs": [
            {
                "goods_id": 145,
                "attr_id": 15,
                "attr_value": "ddd",
                "add_price": null,
                "attr_name": "fffffff",
                "attr_sel": "many",
                "attr_write": "list",
                "attr_vals": ""
            },
            {
                "goods_id": 145,
                "attr_id": 15,
                "attr_value": "eee",
                "add_price": null,
                "attr_name": "fffffff",
                "attr_sel": "many",
                "attr_write": "list",
                "attr_vals": ""
            }
        ]
    },
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

### 编辑提交商品
- 请求路径：goods/:id
- 请求方法：put
- 请求参数

| 参数名             | 参数说明          | 备注            |
| --------------- | ------------- | ------------- |
| id              | 商品ID          | 不能为空`携带在url中` |
| goods_name      | 商品名称          | 不能为空          |
| goods_price     | 价格            | 不能为空          |
| goods_number    | 数量            | 不能为空          |
| goods_weight    | 重量            | 不能为空          |
| goods_introduce | 介绍            | 可以为空          |
| pics            | 上传的图片临时路径（对象） | 可以为空          |
| attrs           | 商品的参数（数组）     | 可以为空          |

- 请求数据
```javascript
{
	"goods_name":"test_goods_name2",
	"goods_price":20,
	"goods_number":30,
	"goods_weight":40,
	"goods_introduce":"abc",
	"pics":[
		{"pic":"/tmp_uploads/30f08d52c551ecb447277eae232304b8"}
		],
	"attrs":[
		{
			"attr_id":15,
			"attr_value":"ddd"
		},
		{
			"attr_id":15,
			"attr_value":"eee"
		}
		]
}
```

- 响应参数

| 参数名          | 参数说明          | 备注                                       |
| ------------ | ------------- | ---------------------------------------- |
| total        | 总共商品条数        |                                          |
| pagenum      | 当前商品页数        |                                          |
| goods_id     | 商品ID          |                                          |
| goods_name   | 商品名称          |                                          |
| goods_price  | 价格            |                                          |
| goods_number | 数量            |                                          |
| goods_weight | 重量            | 不能为空                                     |
| goods_state  | 商品状态          | 商品状态 0: 未通过 1: 审核中 2: 已审核                |
| add_time     | 添加时间          |                                          |
| upd_time     | 更新时间          |                                          |
| hot_mumber   | 热销品数量         |                                          |
| is_promote   | 是否是热销品        |                                          |
| pics         | 上传的图片临时路径（对象） | pics_id:图片ID,goods_id:商品ID,pics_big:大图,pics_mid:中图,pics_sma:小图 |
| attrs        | 商品的参数（数组）     | goods_id:商品ID,attr_value:当前商品的参数值,add_price:浮动价格,attr_vals:预定义的参数值,attr_sel:手动输入，还是单选, |

- 响应数据

```javascript
{
    "data": {
        "goods_id": 145,
        "goods_name": "test_goods_name2",
        "goods_price": 20,
        "goods_number": 30,
        "goods_weight": 40,
        "goods_introduce": "abc",
        "goods_big_logo": "",
        "goods_small_logo": "",
        "goods_state": 1,
        "add_time": 1512962370,
        "upd_time": 1512962370,
        "hot_mumber": 0,
        "is_promote": false,
        "pics": [
            {
                "pics_id": 397,
                "goods_id": 145,
                "pics_big": "uploads/goodspics/big_30f08d52c551ecb447277eae232304b8",
                "pics_mid": "uploads/goodspics/mid_30f08d52c551ecb447277eae232304b8",
                "pics_sma": "uploads/goodspics/sma_30f08d52c551ecb447277eae232304b8"
            }
        ],
        "attrs": [
            {
                "goods_id": 145,
                "attr_id": 15,
                "attr_value": "ddd",
                "add_price": null,
                "attr_name": "fffffff",
                "attr_sel": "many",
                "attr_write": "list",
                "attr_vals": ""
            },
            {
                "goods_id": 145,
                "attr_id": 15,
                "attr_value": "eee",
                "add_price": null,
                "attr_name": "fffffff",
                "attr_sel": "many",
                "attr_write": "list",
                "attr_vals": ""
            }
        ]
    },
    "meta": {
        "msg": "创建商品成功",
        "status": 201
    }
}
```

### 删除商品
- 请求路径：goods/:id
- 请求方法：delete
- 请求参数

| 参数名  | 参数说明 | 备注            |
| ---- | ---- | ------------- |
| id   | 商品ID | 不能为空`携带在url中` |

- 响应数据

```javascript
{
    "data": null,
    "meta": {
        "msg": "删除成功",
        "status": 200
    }
}
```
### 商品图片上传

- 请求路径：upload
- 请求方法：post
- 请求参数

| 参数名  | 参数说明 | 备注   |
| ---- | ---- | ---- |
| file | 上传文件 |      |

- 响应数据

```javascript
{
    "data": {
        "tmp_path": "tmp_uploads/ccfc5179a914e94506bcbb7377e8985f.png",
        "url": "http://127.0.0.1:8888tmp_uploads/ccfc5179a914e94506bcbb7377e8985f.png"
    },
    "meta": {
        "msg": "上传成功",
        "status": 200
    }
}
```

## 订单管理
### 订单数据列表
- 请求路径：orders
- 请求方法：get
- 请求参数

| 参数名                  | 参数说明        | 备注   |
| -------------------- | ----------- | ---- |
| query                | 查询参数        | 可以为空 |
| pagenum              | 当前页码        | 不能为空 |
| pagesize             | 每页显示条数      | 不能为空 |
| user_id              | 用户ID        | 可以为空 |
| pay_status           | 支付状态        | 可以为空 |
| is_send              | 是否发货        | 可以为空 |
| order_fapiao_title   | ['个人','公司'] | 可以为空 |
| order_fapiao_company | 公司名称        | 可以为空 |
| order_fapiao_content | 发票内容        | 可以为空 |
| consignee_addr       | 发货地址        | 可以为空 |

- 响应数据

```javascript
{
    "data": {
        "total": 1,
        "pagenum": "1",
        "goods": [
            {
                "order_id": 47,
                "user_id": 133,
                "order_number": "itcast-59e7502d7993d",
                "order_price": 322,
                "order_pay": "1",
                "is_send": "是",
                "trade_no": "",
                "order_fapiao_title": "个人",
                "order_fapiao_company": "",
                "order_fapiao_content": "办公用品",
                "consignee_addr": "a:7:{s:6:\"cgn_id\";i:1;s:7:\"user_id\";i:133;s:8:\"cgn_name\";s:9:\"王二柱\";s:11:\"cgn_address\";s:51:\"北京市海淀区苏州街长远天地大厦305室\";s:7:\"cgn_tel\";s:11:\"13566771298\";s:8:\"cgn_code\";s:6:\"306810\";s:11:\"delete_time\";N;}",
                "pay_status": "1",
                "create_time": 1508331565,
                "update_time": 1508331565
            }
        ]
    },
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```
