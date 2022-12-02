# iPhone 解锁TikTok/换区/发布视频 + 直播/点赞评论
#摘要
iOS系统版本：16.2 （支持向下兼容）
TikTok版本：Version 27.1.0（前置操作：从 iTunes for Windows V 12.6.5.3 抓包 TikTok Version 21.1.0 安装，登陆后观看视频、直播、评论、点赞、发布视频等模块都正常使用后，再从 App Store 升级至最新版方可使用！）
TikTok TestFlight Version 27.2.0
下载方式：在 美区/日区/台区 App Store 搜索 TikTok 并下载 （港区已停止运营）
支持功能：换区/看视频/发布视频/点赞/评论/TikTok直播
# 准备工作
App Store 下载 TikTok
美区/日区/台区/韩区等 Apple ID、密码 自备
自备 Quantumult X｜Loon｜Surge｜Shadowrocket
可在美区/日区等 App Store 获取
自备代理，ss/ssr/vmess等
# 特别说明
1、为什么要先卸载 TikTok，TikTok 会在第一次使用时触发限制，并导致之后无法通过 MiMt 解密。
2、所以先配置好规则之后，然后在下载 TikTok，减少重定向的请求次数，降低风险，延长规则的寿命。
3、为什么配置好之后还是无法使用，请检查软件的证书有没有安装，信任。 4、或者是 Https 解密（MiMt）与重写（Rewrite）有没有开启。
5、或者是软件是不是盗版，比如用共享 ID 下载的，有设备限制，是无法使用重写脚本功能的。
#Quantumult X
关于换区
解锁并换区：将CN改为想看的国家/地区的2位大写英文简写，
在HTTP复写中，将CN的替换值改为SG、MO、TW等即可换区
#操作步骤
1、打开Quantumult X
2、开启MitM并信任Quantumult X证书： * 设置 → MitM → 开启MitM → 生成密钥及证书 → 右上角点保存 → 允许安装描述文件 → 关闭 → 前往手机的设置，不在Quantumult X了 → 看到已下载描述文件 → 安装 → 输入手机的解锁密码 → 安装 → 安装 → 前往手机的设置 → 通用 → 关于本机 → 证书信任设置 → 找到Quantumult X Custom Root Certificate…点绿它以信任该根证书 → 继续
#方法一：
3、配置文件点击编辑找到[rewrite_remote]添加下面对应国家的复写
日本
https://raw.githubusercontent.com/Semporia/TikTok-Unlock/master/Quantumult-X/TikTok-JP.conf, tag=TikTok, update-interval=86400, opt-parser=false, enabled=true
#方法二：
3、在[rewrite_local]中添加以下重写
(?<=_region=)CN(?=&) url 307 KR
(?<=&mcc_mnc=)4 url 307 2
^(https?:\/\/(tnc|dm)[\w-]+\.\w+\.com\/.+)(\?)(.+) url 302  $1$3
(?<=\d\/\?\w{7}_\w{4}=)1[6-9]..(?=.?.?&) url 307 17
3.1、在[mitm]中添加
hostname = *.tiktokv.com, *.byteoversea.com, *.tik-tokapi.com
# 4、找到[filter_remote]添加下句分流(无论使用方法一或是方法二，此分流都需要添加！)
https://raw.githubusercontent.com/Semporia/TikTok-Unlock/master/Quantumult-X/TikTok.list, tag=TikTok, force-policy=TikTok, update-interval=86400, opt-parser=false, enabled=true
5、换区：在[rewrite_local]中添加下句重写，并将CN改为想看的国家/地区的2位大写英文简写 JP（日本）｜KR（韩国）｜UK（英国）｜US（美国）｜TW（台湾）
(?<=_region=)CN(?=&) url 307 CN
6、开启Quantumult X：前往Quantumult X的主页 → 找到TikTok策略 → 长按添加节点 → TikTok愉快
# Loon
操作步骤
1、打开Loon
2、点击插件在右上角找到➕进去在URL添加想看的对应国家链接,tag处自定义；PROXY 选择TikTok分流策略即可。
3、在[Remote Rule]下面添加TikTok分流规则，示例如下：
https://raw.githubusercontent.com/Semporia/TikTok-Unlock/master/Loon/TikTok.list, tag=TikTok, policy=TikTok, update-interval=86400, enabled=true
# Surge
操作步骤
1、打开Surge
2、点击模块进去添加想看国家的对应模块。
3、添加以下分流
# Shadowrocket
操作步骤
1、打开Shadowrocket
2、开启HTTPS解密并安装、信任Shadowrocket证书： * 配置 → 你使用的配置文件后的i → HTTPS解密 → 开启HTTPS解密 → 生成新的CA证书 → 允许 → 返回点击安装证书，并点击允许 → 前往手机的设置，不是Shadowrocket的 → 看到已下载描述文件 → 安装 → 输入手机的解锁密码 → 安装 → 安装 → 前往手机的设置 → 通用 → 关于本机 → 证书信任设置 → 找到Shadowrocket…点绿它以信任该根证书 → 继续
3、点击配置 → 模块 → 右上角加号，添加想看国家的对应模块。
4、添加以下分流，点击配置 → 你使用的配置后的i → 规则 → 右上角加号 → 类型 → 选择RULE-SET → 策略 → 选择PROXY或者其他你想使用的策略（一般是对应地区的代理服务器节点） → 规则集URL文本框内填写
# 抖音無法觀看
在hostname中加上以下兩條
-*snssdk.com, -*amemv.com
# 抖音IP代理
订阅分流
https://raw.githubusercontent.com/Semporia/Quantumult-X/master/Filter/DouYin.list
