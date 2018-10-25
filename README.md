# 自带 CMS 系统的云转码系统，一体化自动发布云转码 cms 系统

### 开发计划

利用 react native 开发的跨平台原生 APP 代码正在紧锣密鼓的准备中，大概 15 天会第一个基础版本。大家敬请期待。

### 最新多端视频套件正式发布

#### 套件图示：

![视频多端套件](https://images.gitee.com/uploads/images/2018/1023/175945_1be1e689_145248.jpeg "未标题-1.jpg")

##### 涉及源码：

- express-ffmpeg: [https://gitee.com/quazero/express-ffmpeg](https://gitee.com/quazero/express-ffmpeg)
- cdn-manager: [https://gitee.com/quazero/cdn-manager](https://gitee.com/quazero/cdn-manager)

##### 演示链接：

- Topercms: [https://cms.moejj.com](https://cms.moejj.com)
- cdn 处理演示：
- 原图片：https://www.moejj.com/videos/5bc721ef87af60065e31735e/1.jpg 1280\*720
- cdn 处理图片：https://cdn.moejj.com/poster/videos/5bc721ef87af60065e31735e/1.jpg 400\*300jpg 质量 90%
- APP 正式上线，安卓测试版本下载地址：https://cms.moejj.com/expressffmpeg.apk
  苹果需要翻墙才能安装，暂时没有构建。

##### 说明

- 这套 CMS 可能是国内最具实验性的 CMS，完全利用云转码的 API 进行调用，并且使用服务端渲染技术，页面自动缓存和预加载技术，利用 vuejs+nuxtjs+elementui+vuetify 进行编写，类似 youtube 和腾讯视频、花瓣的技术。
- app 采用 react-native 编写，多端共用一套源码，构建出来的 APP 具有跟原生代码编写的 APP 同样的效能和体验，让使用者体验保持在 60 帧的完美原生 APP 体验。

### 2018 年 9 月 4 日大更新

这次完全更改了项目了定位，云转码不再是简单的云转码系统，而是 CMS 系统+云转码系统一体化，自带整个完备的并且对移动端友好的，而且非常利于 SEO 优化的自适应 CMS 系统，根据后台的分类系统和门户 CMS 管理系统，直接在首页达成完备的在线视频播放系统，适用于在线教育、企业内部培训视频、在线视频自媒体门户等多种运用方向。这次更新完善了视频的分类系统，完善了视频的搜索功能。CMS 现在集成有视频发布，文章发布和图集发布三个功能。

### 增加会员系统

增加会员系统，可以不开启 CMS，独立开启会员系统，双向验证，安全可靠，后台可以配合卡劵生成，前台用户使用卡劵进行升级。

### 真正意义上的权限系统

**路由层面的权限系统**，非网上的播放器假权限，根据权限不同，相同的 M3U8 播放文件返回不同的内容，比如普通会员只能播放 3 分钟，就只会返回 3 分钟的切片内容，升级之后才会返回完整的切片内容。

### 卡劵系统

后台设定卡劵生成，可以设置开通会员时间，用户前台使用即可升级到对应的会员，到期之后权限失效，需要重新开通，如果连续使用则是累加会员时间。

#### 项目介绍

主要实现功能：
一、视频批量上传，视频分块上传。
二、视频批量转码并且切片，切片完成删除原视频文件。
三、视频批量添加水印。
四、一键获取分享链接，防盗链设置，只允许指定域名 ifream 调用，token 防盗链等。
五、自带完备的 CMS 系统。

- 官网地址：[https://ffmpeg.moejj.com](https://ffmpeg.moejj.com)
- 演示站：[https://www.moejj.com](https://www.moejj.com)
- 云转码专用 CMS：[https://cms.moejj.com](https://cms.moejj.com)
- 目前码云的安装教程是最正确的，安装请参照码云的安装教程。

本开源项目采用 nodejs、expressjs、mongodb 开发。
使用前请安装 ffmpeg。

#### 软件架构

nodejs v8.7.0 版本
expressjs 4.16.0 版本
mongoDb
ffmpeg 3.4.1 版本
Linux 系统上运行完美。

#### 安装教程

##### 自己编译

1. 安装 ffmpeg
   Ubuntu16.04 安装方法：

```
sudo add-apt-repository ppa:djcj/hybrid
sudo apt-get update
sudo apt-get install ffmpeg
```

然后输入 ffmpeg 和 ffprobe 查看是否安装成功。

2. 安装 nodejs、expessjs、mongodb、redis 环境。
   详情见：[express+nodejs+redis+mongodb+pm2+nginx 环境部署安装，生产环境及开发环境部署](http://blog.sina.com.cn/s/blog_13e807ed00102wlxo.html)

3. node ./bin/www
   访问 localhost:3000/server
   登陆账号密码在/config/auth.js 中设置

4. ffmpeg 烧录字幕的时候会查找字体配置文件，/etc/fonts，如果里边没有 fonts.conf，请将本源码中 fonts.conf 上传到/etc/fonts，有些 linux 系统没有中文字体支持，请将 msyh.ttf 上传至/usr/share/fonts 里边。

##### 利用 sh 文件安装

- ./install.sh 使用前请给予权限。(已经弃用，请前往官网按步骤安装)

#### 使用说明

1. 创建/config 文件夹并在里边创建 auth.js 文件
   代码如下：

```
module.exports = {
    user: "username",
    password: "password",
    db: "dbname",
    dbuser: "dbuser",
    dbpassword: "dbpassword",
    secret: "yoursecret",
    login: "/adminloginurl",
    loginmsg: "404 Not Found"
};
```

**注意：**很多用户安装出错就在这里，比很早的版本多了三个设置项，secret 是 session 需要的秘钥，login 是后台登陆地址，loginmsg 是后台未登录显示的内容，默认是 404。

2. 登陆后台之后请立刻在设置中进行设置。
3. 上传视频即可上传视频。
4. 转码页面一键转码。
5. 支持后台字幕上传，名称与视频名一致，则系统会自动烧录字幕。例如：aaa.mp4，则 srt 字幕名为 aaa.srt。
6. 支持一键入库，利用 ftp 等工具将视频上传至 movies 文件夹，后台可以一键入库，进行转码切片操作。
7. 秒切功能，开启之后，无需进行转码的视频会直接切片。（后台可设置）

#### 版本

##### V5.1 版本

- 更新最新的有用的 p2p 模块，参照https://github.com/cdnbye/hlsjs-p2p-engine进行配置
- 对接 CMS 和 APP 完成，demo 正在制作中。

##### V5 版本

- 增加后台登陆地址修改功能，增加后台访问提示信息功能。
- 增加视频总量和未完成、完成的统计功能。
- 增加大量 API，为 APP 做准备，APP 已经出了原型，最近会放出 demo 安装包。
- APP 和新型超级 CMS 正在配套完善中。
- express-ffmpeg 进化成为跨平台多端产品。

##### V4.3 版本

- 增加批量切片头的功能，选择视频，设置时间轴，一键切片头，利用速度最快的参数，秒切片头。
- 增加 m3u8 开放浏览功能，设置里边删除 key，则 m3u8 开放浏览，可以分享到任何播放器进行播放，如果设置了 key，则可以使用 m3u8api 调用，安全性更高。
- 修复转码切片核心源码中的一个 bug，此 bug 会导致切片时候之后转码也会失败，推荐更新。

##### V4.2 版本

- 更新了上传封面功能，可以独立为视频上传封面，没有上传封面就会使用截图做封面。
- 增加了 M3U8 的 api 功能，直接填入需要输入 m3u8 的地方就可以直接调用 m3u8，此 api 仅支持 H5 播放器，ckplayer 等 flash 播放器不支持，并且需要 nginx 的正确配置。
- 引入 redis 缓存机制，有些页面需要大量计算的地方，通过 redis 缓存速度大增，后期可以为分布式做准备。
- CMS 首页更改为 2 列排序，手机上的效果更好。
- 因为 bootcss 的 CDN 爆炸，已经把所有 cdn 上的 JS 和 css 全部更改为本地。

##### V4.1 版本

- 优化分类引用防盗链控制的逻辑，增加单分类开放浏览的选项。
- 优化后台视频管理数量选择，和一键批量修改。
- 后台增加设置选项，设置引用盗链跳转链接。
- 图集页展示更加完美。

##### V4 版本

- 大更新，CMS 怎么能没有图集发布和文章发布，这次更新增加图集和文章发布的完整支持。
- 图集发布，一键上传图片，一键完成封面截图，一键前端展示，点击翻页。
- 文章发布，集成 editor.md，markdown 编辑器，极其完美的书写体验。
- 增加分类编辑，编辑中可以针对分类添加防引用盗链，盗链功能颗粒化管理。
- 电影管理页，增加一键修改所有电影分类的功能。
- 增加播放器文字水印广告背景色和背景透明度设置。
- 完全重写分享页面的代码，速度更快。

##### V3.2 版本

- 增加播放器进度条预览效果，鼠标移动到进度条会显示对应时间轴的预览图。
- 增加后台设置 TS 加密，设置加密之后，切片文件 TS 会全部加密。
- Ts 加密高级特性，每一个视频都对应一个独立的 KEY 文件，安全性大涨。
  ![输入图片说明](https://images.gitee.com/uploads/images/2018/0920/212642_dc2f0ad0_145248.png "屏幕快照 2018-09-20 下午7.22.39.png")
  ![输入图片说明](https://images.gitee.com/uploads/images/2018/0920/212650_285c80e9_145248.png "屏幕快照 2018-09-20 下午9.21.22.png")

##### V3.1 版本

- 增加队列转码功能，先上传的先转码，循环处理，转码失败会自动跳过
- 增加后台统计代码功能，可以添加第三方统计代码，分享链接和 CMS 单独设置
- 修复会员开通卡劵之后，m3u8 浏览器缓存问题

##### V3 版本

- 市面上唯一的路由层面的权限控制
- 完备可扩展的会员系统
- VIP 卡劵后台一键生成
- **根据权限不同，相同 M3u8 文件动态生成不同的内容**

##### V2.1 版本

- 增加防盗链域名多域名支持
- 针对手机 QQ 浏览器优化，支持显示播放器水印广告和文字链接广告
- 增加图表统计页面，炫酷图表统计和表格统计。
- 增加 P2P 功能，待测试效果。

##### V2 版本：

- 大更新，增加门户 CMS 设置，内嵌 CMS 系统
- 增加播放器配置
- 播放器图片水印和文字广告
- 播放页面完全自定义图片水印和文字广告

##### V1.5 版本：

- 完全重构 ffmpeg 相关的所有代码。
- 将转码和切片合并成一次操作，提升双倍效率，原来是转码成 mp4，然后再 mp4 切片。
- 完全重写切片代码，秒切的速度提升超过 10 倍，1G 视频切片完成只需要半分钟。

##### V1.4 版本：

- 增加了 1080P 的选项。
- 增加切片 ts 域名分发，负载均衡的功能。
- 开启域名分发，数台服务器同步切片内容，访问 m3u8 动态生成循环域名切片前缀。

##### v1.3 版本：

- 更改播放器为 Dplayer 播放。
- 增加 VTT 字幕支持，后台可以给视频分别上传 vtt 字幕，前台播放会自动加载，支持了字幕和视频分开。
- 增加一个 webtorrent 功能（测试玩），地址：yourdomain/playmagnet。

##### v1.2 版本：

- 增加批量烧录字幕功能，支持 srt 字幕，改成和视频名一样，系统在转码的时候会自动把字幕烧录进去。如果存在 srt 字幕文件，则对应电影无论是否设置秒切都会进行转码。
- 增加批量入库功能，利用 ftp 或者其他工具将视频传至 movies 文件夹，在后台即可一键入库。
- 增加秒切功能，后台设置开启，即视频如果小于设置的分辨率并且编码为 h264 则会跳过转码直接切片。
- 增加自动生成截图功能，默认 4 张截图，路径 yourdomain/videos/:id/(1|2|3|4).jpg。

##### v1.1 版本：

- 批量上传视频，大文件切片上传。
- 批量转码并切片。
- 设置防盗链和分辨率，添加水印，一气呵成。

#### 截图

![图集展示](https://images.gitee.com/uploads/images/2018/0927/104338_617a2992_145248.jpeg "FireShot Capture 5 - 热血动漫角色大集合 I 新的在线教育 - http___localhost_3000_image_5baa513d0046647562fb1e0c_1.jpg")
![文章列表](https://images.gitee.com/uploads/images/2018/0925/232417_da13c156_145248.png "FireShot Capture 1 - 文章 - 新的在线教育 - http___localhost_3000_articles.png")
![图集](https://images.gitee.com/uploads/images/2018/0925/233414_4ffade89_145248.jpeg "FireShot Capture 2 - 图集 - 新的在线教育 - http___localhost_3000_imageslist.jpg")
![视频](https://images.gitee.com/uploads/images/2018/0925/233446_1f357ab5_145248.jpeg "FireShot Capture 3 - 新的在线教育 - http___localhost_3000_.jpg")
![输入图片说明](https://images.gitee.com/uploads/images/2018/0904/192833_58d6b693_145248.jpeg "FireShot Capture 3 - 在线教育，美丽人生 - http___localhost_3000_.jpg")
![输入图片说明](https://images.gitee.com/uploads/images/2018/0904/192842_6a95e52a_145248.jpeg "FireShot Capture 4 - 门户cms设置 - http___localhost_3000_admin_portal.jpg")
![输入图片说明](https://images.gitee.com/uploads/images/2018/0904/192851_cfc5123c_145248.jpeg "FireShot Capture 5 - 分类管理 - http___localhost_3000_admin_categories.jpg")
![输入图片说明](https://images.gitee.com/uploads/images/2018/0904/192907_42fa526f_145248.jpeg "FireShot Capture 6 - 全部电影库 - http___localhost_3000_admin_movies.jpg")
![输入图片说明](https://images.gitee.com/uploads/images/2018/0904/192931_5918d089_145248.jpeg "FireShot Capture 8 - [喵萌奶茶屋][繁体中文][与僧侣交合的色欲之_ - http___localhost_3000_movie_5b8e49643c3ee95a185469a7.jpg")
![输入图片说明](https://images.gitee.com/uploads/images/2018/0915/092922_4ab46535_145248.jpeg "屏幕快照 2018-09-15 上午9.26.56.jpg")
![输入图片说明](https://images.gitee.com/uploads/images/2018/0915/092907_0ce6f5d8_145248.jpeg "屏幕快照 2018-09-15 上午9.26.48.jpg")
![输入图片说明](https://images.gitee.com/uploads/images/2018/0915/092858_2ba6278d_145248.jpeg "屏幕快照 2018-09-15 上午9.26.38.jpg")
![图表统计](https://images.gitee.com/uploads/images/2018/0913/144939_3ba18b3c_145248.jpeg "屏幕快照 2018-09-13 下午2.46.55.jpg")
![输入图片说明](https://images.gitee.com/uploads/images/2018/0910/120203_ea18551d_145248.png "播放器设置 - http___localhost_3000_admin_bofangqi.png")
![ts文件域名分发](https://images.gitee.com/uploads/images/2018/0731/102414_be8e1a72_145248.jpeg "屏幕快照 2018-07-31 上午10.18.51.jpg")
![上传截图](https://gitee.com/uploads/images/2018/0606/185630_b769b67c_145248.jpeg "屏幕快照 2018-06-06 下午6.55.28.jpg")
![设置](https://images.gitee.com/uploads/images/2018/0731/102525_c3f5c8ae_145248.jpeg "屏幕快照 2018-07-31 上午10.18.37.jpg")

有问题请联系我，q 195996048，邮 mwm0022@qq.com
