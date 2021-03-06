# describeSecrets


## 描述
查询 secret 列表。<br> 
此接口支持分页查询，默认每页20条。


## 请求方式
GET

## 请求地址
https://nativecontainer.jdcloud-api.com/v1/regions/{regionId}/secrets

|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**regionId**|String|True| |Region ID|

## 请求参数
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**pageNumber**|Integer|False| |页码；默认为1|
|**pageSize**|Integer|False| |分页大小；默认为20；取值范围[10, 100]|
|**filters**|Filter[]|False| |name - secret名称，支持模糊搜索<br>|

### Filter
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**name**|String|True| |过滤条件的名称|
|**operator**|String|False| |过滤条件的操作符，默认eq|
|**values**|String[]|True| |过滤条件的值|

## 返回参数
|名称|类型|描述|
|---|---|---|
|**result**|Result| |
|**requestId**|String| |

### Result
|名称|类型|描述|
|---|---|---|
|**secrets**|Secret[]| |
|**totalCount**|Number| |
### Secret
|名称|类型|描述|
|---|---|---|
|**name**|String|机密数据名称|
|**secretType**|String|私密数据的类型，目前仅支持如下类型：docker-registry：用来和docker registry认证的类型|
|**createdAt**|String|创建时间|
|**data**|DockerRegistryData|机密的数据|
### DockerRegistryData
|名称|类型|描述|
|---|---|---|
|**server**|String|registry服务器地址|
|**username**|String|用户名|
|**password**|String|密码|
|**email**|String|邮件地址|

## 返回码
|返回码|描述|
|---|---|
|**200**|OK|
|**400**|Invalid parameter|
|**401**|Authentication failed|
|**404**|Not found|
|**500**|Internal server error|
|**503**|Service unavailable|
