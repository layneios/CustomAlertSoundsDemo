# CustomAlertSoundsDemo
项目中遇到需要自定义通知声音的需求，以前没做过，就查了下[官方文档](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/IPhoneOSClientImp.html#//apple_ref/doc/uid/TP40008194-CH103-SW6)，就像文档上说的，实现起来确实挺简单，就整理下当做备忘吧。

关于推送，官方文档、各种第三方推送文档都很全，就跳过了。

由于自定义通知声音还是由 iOS 系统来播放的，所以对音频数据格式有限制，可以是如下四种之一：

1. Linear PCM
2. MA4 (IMA/ADPCM)
3. µLaw
4. aLaw

对应音频文件格式是 `aiff`，`wav`，`caf` 文件，文件也必须放到 app 的 `mainBundle` 目录中。

自定义通知声音的播放时间必须在 30s 内，如果超过这个限制，则将用系统默认通知声音替代。

可以使用 `afconvert` 工具来处理音频文件格式，在终端中敲入如下命令就可以将一个 `mp3` 文件转换成 `caf` 文件：

```
afconvert unbelievable.mp3 unbelievable.caf -d ima4 -f caff -v
```

转换完成后就可以将 `unbelievable.caf` 这个文件拖入 Xcode 工程中，编译运行项目在真机上。

![将 unbelievable.caf 文件拖入工程中](http://lengmolehongyan.github.io/images/QQ20151226-0@2x.png)

发送推送通知时，只需配置 `sound` 字段的值为导入到工程中的音频文件名，这里即就是 `unbelievable.caf`。

测试~~，完美！！！收到推送时，通知声音就是我们自定义的声音了。

![收到推送信息](http://lengmolehongyan.github.io/images/QQ20151226-1@2x.png)

