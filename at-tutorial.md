#使用AT固件
- 下载AT固件](https://github.com/pushdotccgzs/es-push-doc/raw/master/at-push.zip)
- 刷入板子
- 开启调试控制台，按以下方式输入指令：
```
//注解，以下以 「>」开头的为输入行，已「<」开头的为输出行，其余为注解
>AT

<OK
>AT+CWMODE=1

<OK
//请配置为正确的SSID与密码，并能连入网络。
>AT+CWJAP="OUR_SSID","PWD_SSID"

<OK
>AT+CIPSTA?
<+CIPSTA:"192.168.0.102"

<OK
>AT+PUSH?
<3

<OK
//以下请替换为你自己添加的APPID与APPKEY
>AT+PUSH=APPID,APPKEY

<OK
//若过较长时间仍一直返回3，则无法连接到服务器，请AT+RST后重试
>AT+PUSH?
<2

<OK

+MSG,20:HELLO，FROM PUSHMSG.
```

