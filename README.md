# 群发邮件脚本

## 初次配置

1. 在`main.py`文件中设置变量`FROM_ADDR`，`FROM_ALIAS`，`PASSWORD`，`SERVER`。需要注意的是`PASSWORD`对于某些邮箱，是邮箱授权码(比如qq邮箱)。

2. 在`assets/list.xlsx`文件中设置需要群发的邮箱列表。`to`表示收件人，`cc`表示抄送人。一般情况下，直接按照样例文件设置即可(全部设置为`to`，不设置`cc`)。

## 发送邮件

一条命令即可发送邮件。

  ```python
  $ python main.py -s '题目20210925进展汇报' -c '邮件正文内容.txt' -a '附件20210925.pptx'
  ```

## 参数列表

|参数|类型|含义|
|:---|---|---|
|`-s`, `--subject`|字符串|邮件主题|
|`-c`, `--content`|字符串(txt文件路径)|邮件正文(目前仅支持txt，即纯文本)|
|`-a`, `--attachment`|字符串(任意类型的文件路径)|邮件附件|

## TODO

> 如果有时间就更新，没时间的话就鸽了。欢迎issue或者pr :-)

- [ ] 没有附件的时候也应该正常发送，因此需要判断附件那一项是否为空，如果不为空，判断文件路径是否存在。如果存在就发送，否则报错并退出。并且要注意，“没有附件”和“附件名字敲错”是两个不同的概念。当没有附件时，意味着没有flag，此时正常发送。当附件名字敲错时，应该立刻报错。
- [ ] 对于邮件正文，如果只是简单的一段话，应该不用再非得找对应的txt文件了，直接发送这段话就可以。所以先判断正文是否对应一个文件。如果不对应一个文件，则直接发送这段话。但这是一项危险操作。因此需要给一个选项，让用户决定是否启用这个功能。
- [ ] 不应该总是更改源代码，而是提供一个配置文件让用户修改。并且用户配置文件和邮件列表文件最好全换成json格式。
- [ ] 加入定时功能，到某个时间自动发邮件。但是这需要使用一个服务来保持唤醒状态，并且最好在linux下面启动一个服务。因此考虑通过一个服务来管理多个用户的邮件群发。但这又涉及到隐私安全问题，目前不太容易解决。