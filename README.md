# hugo-pacman-theme

http://fancygo.cn

## config.toml

```toml
BaseURL = "http://fancygo.cn/"
LanguageCode = "zh-CN"
HasCJKLanguage = true
Title = "FancyGo"
Theme = "fancy"
pygmentsStyle = "default"
pygmentsUseClasses = true

[Author]
  Name = "FancyGo"

[outputs]
  home = [ "RSS", "HTML" ]
    
[outputFormats] 
  [outputFormats.RSS]
    mediatype = "application/rss"
    baseName = "feed"

[Params]
  Author = "FancyGo"
  AuthorHomepage = "http://fancygo.cn"
  BottomIntroduce = "Linux 爱好者 <br/> Go 爱好者"
  Description = "Description"
  Subtitle = "subtitle"
  Weibo = "weibo"
  WeiboID = 0000000
  Twitter = "twitter"
  GitHub = "github"
  Facebook = "facebook"
  LinkIn = "linkin"
  Imglogo = "img/fancy.jpg"
  AuthorImg = "img/fancy.jpg"
  DateFormat = "2006年01月02日"
  MonthFormat = "2006年01月"
  FancyBox = true

  [Params.GoogleAnalytics]
    ID = ""

  [Params.Disqus]
    ShortName = "fancygo"

  [Params.Strings]
    Search = "搜索"
    PageNotFound = "你访问的页面不存在"
    ShowSideBar = "显示侧边栏"
    HideSideBar = "隐藏侧边栏"
    Categories = "分类"
    Archive = "归档"
    Tags = "标签"
    TagCloud = "标签云"
    Rss = "RSS 订阅"
    TableOfContents = "文章目录"

[Menu]
  [[Menu.Main]]
    Name = "首页"
    URL = "/"
    Weight = 1
  [[Menu.Main]]
    Name = "关于"
    URL = "/about"
    Weight = 2
```
