# API 约束规范

## 1. 协议标准
- **通信协议**：HTTPS
- **数据格式**：JSON
- **字符编码**：UTF-8

## 2. 接口定义风格 (RESTful)
- **GET** `/api/v1/resources` - 获取列表
- **GET** `/api/v1/resources/:id` - 获取详情
- **POST** `/api/v1/resources` - 创建
- **PUT** `/api/v1/resources/:id` - 全量更新
- **PATCH** `/api/v1/resources/:id` - 部分更新
- **DELETE** `/api/v1/resources/:id` - 删除

## 3. 通用响应结构
```json
{
  "code": 200,
  "message": "success",
  "data": { ... }
}
```

## 4. 错误码定义
| 错误码 | 说明 |
| :--- | :--- |
| 400 | 请求参数错误 |
| 401 | 未授权 |
| 500 | 服务器内部错误 |
