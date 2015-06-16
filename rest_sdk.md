#服务端接口


espush使用的服务端接口与其他推送平台如[信鸽](http://xg.qq.com/)等类似，简述如下

##协议整体描述
请求URL结构为：`http://接口域名/openapi/接口命令/?接口参数`。其中，接口域名暂时使用IP为`211.155.86.145:8000`，后期可能改为域名的方式。接口命令参考`现有接口`，接口参数根据不同的接口有不同的参数，同时还有通用参数。

##通用参数
| 参数命名|    参考取值| 说明|
| :-------- | --------:| :--: |
| appid|100000    |  平台设备类别APP，数字型|
| timestamp| 1434447718  |  10位的Unix时间戳 |
| sign|    32位md5后的字符串，小写| 签名参数，参考`签名认证方式`|

###签名认证方式
内容签名sign的计算方法如下：

- 提取请求的方法本身的小写字母表示，如`get`, `post`等，记作字符串A
- 提取请求的其他参数（GET与POST参数均需要，COOKIES参数不计入，但不包括sign），并按Key-Value的形式并转换为小写字母表示（未做urlencode），再按Key的降序排列，组成如下形式：`key3=v3&key2=v2&key1=v1`，此处记作字符串B
- 提取APPKEY，记字符串C
- Sign的值为 S = MD5(A+B+C)

如POST请求，APPID为1234，APPKEY为25b28f0ffb9711e4a96d446d579b49a1，无其他额外的请求参数，则只有通用参数appid、timestamp与sign，则字符串S应为:`gettimestamp=1433814203&appid=123425b28f0ffb9711e4a96d446d579b49a1`,对齐进行MD5运算，取运算后的小写字母表示，即得到最终sign值:`9f0b613de12d5bb0451c556900a39559`

##通用返回
使用HTTP返回码，如5XX代表服务端的错误，4XX代表客户端的错误，通常401是sign取值错误，400是参数缺失，404是对应资源找不到。
##现有接口
###/openapi/apps/
功能：
方法：
参数：
返回：
###/openapi/devices/list/
功能：
方法：
参数：
返回：
###/openapi/device/:devid/message/
功能：
方法：
参数：
返回：
###/openapi/app/:appid/message/
功能：
方法：
参数：
返回：
###/openapi/up_messages/
功能：
方法：
参数：
返回：
###/openapi/push_messages/
功能：
方法：
参数：
返回：


