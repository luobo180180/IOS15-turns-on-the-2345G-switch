# IOS15-turns-on-the-2345G-switch
filza开运营商2345G开关，并且可以切换网络，使用效果如图1.2.3.4.5所示。

测试环境：

iOS15.4

双卡中国移动

测试结果

除3G开关选择无效外，其它均可以正常切换使用。（可能我这里没有移动3G信号，联通有3G）

如果已越狱的设备请直接安装3个插件即可实现。未越狱也没安装trollstore无法实现，抱歉，可以不用看了。
已安装trollstore的ios15-ios15.4.1系统请继续往下看（iOS 14未测试）。

本方法教程需要一定的动手能力，小白请谨慎尝试。

所需工具：

filza

第一步：找到运营商版本号
打开系统设置-通用-关于本机 查看当前运营商版本号，并记住这个版本号（比如楼主的是默认50.0，如果用52.0成功率比较低），后面需要用到

第二步：确定plist文件
用filza打开路径var/mobile/Library/Carrier Bundles/Overlay目录下看到下面有多个以（为了安全起见，建议先备份此文件夹）如图6
device+carrier+46000+D53gxxxxxx+50.0.plist
device+carrier+46000+D53gxxxxxx+51.0.plist
device+carrier+46000+D53gxxxxxx+52.0.plist
device+carrier+46001+D53gxxxxxx+50.0.plist
device+carrier+Default+D53gxxxxxx+50.0.plist
类似这样的文件，备份好后，下面两种方法确定plist文件1和2，你选择其一。

1.我们全部删除Overlay下的所有文件，然后重启手机再次进入var/mobile/Library/Carrier Bundles/Overlay目录下
这里会看到最多2个文件（非Default就是），那就是我们需要操作的plist文件。

2.根据下面这个表找到我们需要操作的文件，比如楼主的是中国移动的

运营商代码：
46000 中国移动（GSM）
46001 中国联通（GSM）
46002 中国移动（TD-S）
46003 中国电信（CDMA）
46004 空（似乎是专门用来做测试的）
46005 中国电信（CDMA）
46006 中国联通（WCDMA）
46007 中国移动（TD-S）
46008
46009
46010
46011 中国电信（FDD-LTE）

得到移动是46000，然后通过之前看到的运营商版本号是50，那么后面的数字50.plist
那么device+carrier+46000+D53gxxxxxx+50.0.plist就是楼主确定好的plist文件。
确定好文件后

小实验确认plist文件是否选择正确
你filza默认打开device+carrier+46000+D53gxxxxxx+50.0.plist文件，运营商版本大于50.0的请把ShowVolteSwitch打开，然后重启手机后看看 设置-蜂窝网络-蜂窝号码-语音与数据 是否有VOLTE开关，如有就是这个文件，反之关闭可以隐藏这个按钮。

第三步：替换代码（这步比较难，很多锋友被卡在这步）
下载分享文件里的：2345G.zip解压后的开2345G.plist 然后把这个2345G.plist复制到手机里用filza点2345G.plist后面的感叹号-点右上角的 其它打开 方式选择 文本编辑器 然后复制里面的<dict>到</dict>的全部开关代码 如图7（教程底部有贴出复制内容部分）
然后回到filza点\var\mobile\Library\Carrier Bundles\Overlay文件夹下 你确认的运营商plist文件 如楼主的：device+carrier+46000+D53gxxxxxx+50.0.plist后面的感叹号 如图8
在点右上角的箭头 如图9，选择文本编辑器打开 如图10，找到IMSConfig位置，如图11
然后替换掉图片中框选部分的代码，最后点右上角 的储存-左上角完成。

第四步：再次点 确定好的plist文件 device+carrier+46000+D53gxxxxxx+50.0.plist 如图12（在12楼） 后面的感叹号在访问权限点粘贴-在隐藏这里填0555后保存退出，最后重启手机后查看效果，如果已开启2345G开关，则无需第五步。
如果没出开关，也确定小实验确认plist文件是选择正确的，继续第五步。

第五步：下载分享文件里的data.tar，用爱思传到手机文档里，解压date得到一个var目录，进入该目录\var\mobile\Library\Carrier Bundles\下看到iPhone文件夹，把这个文件夹复制到你手机根目录下\var\mobile\Library\Carrier Bundles\里覆盖原iphone文件夹即可，再次重启手机看效果。

问答
问：为什么我替换了，重启后没有效果
答：1.很多时候是确认文件不对导致，建议用第二步的第1种方法，这样重新生成的文件一般是准确的。
然后你filza默认打开，把ShowVolteSwitch和ShowVolteWarningUnsupportedCarrier打开，然后重启手机后看看是否有VOLTE开关，如有就是这个文件。
如果没有就不是，那你可能说，我这个Overlay文件夹下没有其它文件啦？现在你把Overlay文件夹下所有文件删除，然后设置-通用-传输或还原iPhone-还原-还原网络设置，重启手机再次进入Overlay目录即可看到。
2.尝试第五步。

问：越狱的手机可否安装插件的方式
答：请打开楼主分享的文件com.yourepo.itweakios.carriercrack-globalios14_1.开2345G开关.deb，安装即可。


附件：
https://wwn.lanzouj.com/b01vw53ra
密码:cy54

楼主IOS15.4中国移动50.0运营商已做好的文件（下载后直接放\var\mobile\Library\Carrier Bundles\Overlay目录里，覆盖原文件，重启手机即可）

第三步说的<dict>到</dict>的全部开关代码如下
	<key>DefaultWhenImsSwitchOff</key>
	<integer>0</integer>
	<key>DerPriFileVersion</key>
	<string>0.1.163</string>
	<key>Enable4GByDefault</key>
	<true/>
	<key>Show3GSwitchWith5G</key>
	<true/>
	<key>Show5GStandaloneSwitch</key>
	<true/>
	<key>Enable5GStandaloneByDefault</key>
	<true/>
	<key>ShowHighDataModeSwitch</key>
	<true/>
	<key>IPv6SupportedDataModeMask</key>
	<integer>110620</integer>
	<key>ShowVolteWarningUnsupportedCarrier</key>
	<true/>
	<key>IgnoreDSDForUI5G</key>
	<true/>
	<key>Show4GSwitch</key>
	<true/>

如何还原所有设置（还原后可以升级运营商）
用filza打开\var\mobile\Library\Carrier Bundles目录，删除该目录下所有文件
然后设置Carrier Bundles文件夹权限为0755，然后重启两次手机，记得是重启两次
重启第一次会恢复LTE信号，再次重启才会恢复5G信号，此时升级刷IPCC有效。

如果上诉方法不行，请设置-通用-传输或还原iPhone-还原-还原网络设置
