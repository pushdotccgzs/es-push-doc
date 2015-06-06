#使用esp-sdk开发
首先当然是clone 项目https://github.com/pushdotccgzs/espush_sdk

本质上，我的工作只是在官方sdk上新增了库文件libpush.a，并修改其makefile而已，官方最新版SDK于此：http://bbs.espressif.com/viewtopic.php?f=5&t=481&sid=2b010931ef357b2847f14a6f012e2d84

客户端的使用方式极为简单，克隆此[github库](https://github.com/pushdotccgzs/esp_push_example)，使用

`make clean && make BOOT=new APP=1`

即可编译出user1，同理使用

`make clean && make BOOT=new APP=2`

即可编译出user2.

本质上只是在[乐鑫官方库](http://bbs.espressif.com/viewtopic.php?f=5&t=321)的基础上增加了用于推送的`libpush`库，如果开发者使用如安信可IDE等，可直接编译出对应的flash rom。

