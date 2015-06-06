#使用AT固件
- 下载AT固件
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


如果您只是将ESP8266芯片用作您的网络用途，那AT固件是您最好的选择，点击此处下载ES-PUSH的AT固件，并按下图所示刷入您的设备中。

AT-PUSH固件新增了3个命令，以下做简要说明
- AT+PUSH，使用AT+PUSH?可查询当前连接状态，返回值定义为：
```
CONNECTING = 0
DNS_LOOKUP = 1
CONNECTED = 2
DISCONNECTED = 3
```
留意只有返回值为 `2` 时才代表已连接，其余都是未连接状态，如连接中，DNS查找中，已断开等。

同时，使用`AT+PUSH=APPID,APPKEY`可连入ES-PUSH系统。命令为异步式，敲入后立即返回，可随时使用AT+PUSH?查询连接状态，当处于可连接时，能使用如下命令。
- AT+PUSHMSG，数据推送，距离推送HELLO字符串到服务器可发送指令`AT+PUSHMSG=HELLO`即可。在与服务器正常连接的情况下返回OK，否则返回ERROR。

- AT+UNPUSH，使用此命令断开与服务器的连接，断开后服务端也将无法推送数据到终端。返回OK。
- +MSG，收到数据后，模块将向串口写入以下数据，数据已`+MSG %d:`开头，其中%d为


