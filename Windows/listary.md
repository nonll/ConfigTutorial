## 关键字
### Web搜索
> 添加方式，批量添加， 单个添加

> 示例：
 `关键字 | 名称 | URL`

1. 淘宝 --> 淘宝搜索并按销量排序

`淘宝 | 淘宝 for '{query}' | http://s.taobao.com/search?q={query}&sort=sale-desc`

2. 京东 --> 搜索并自动勾选销量排序+京东自营+有货
`京东 | 京东 for '{query}' | https://search.jd.com/Search?keyword={query}&enc=utf-8&qrst=1&rt=1&stop=1&vt=2&wq={query}&psort=3&wtype=1&stock=1&click=2`

3. 天猫 --> 搜索并按销量排序
`天猫 | 天猫 for '{query}' | https://list.tmall.com/search_product.htm?q=%{query}&sort=d&styler`

4. 慢慢买比价
`bj | 慢慢买比价 for '{query}' | http://s.manmanbuy.com/Default.aspx?key={query}`

5. 使用谷歌在百度网盘里搜索格式为 pdf 或 mobi 格式的书籍
`spdf | 百度网盘电子书 for '{query}' | https://www.google.com/#newwindow=1&q={query}+pdf+OR+mobi+site:pan.baidu.com`

6. 搜盘网
`sp | 搜盘网 for '{query}' | http://www.soupan.info/search.php?q={query}`

7. 字幕组
`zm | 字幕组 for '{query}' | http://www.zimuzu.tv/search/index?keyword={query}&search_type=`

### 自定义
> 示例：
 `关键字 | 名称 | 路径 | 参数`

1. 调用GoldenDict快速查词
 `gd | GoldenDict | 路径 | {query}`
 
2. 调用everything进行全盘搜索
`e | everything全盘搜索 "{query}" | D:\Special\Scoop\apps\everything\current\Everything.exe | -search {query}`

3. 调用filelocator进行全文搜索
 `fl | FileLocator全文搜索 "{query}" | 路径 | -c {query}`

## 动作
