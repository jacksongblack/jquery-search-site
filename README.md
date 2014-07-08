## 静态页面页面全站搜索jquery插件

 本插件作为jquery插件，使用XML作为数据原始数据，最初设计于使用github的jekyll作为博客站点，我的博客[我是链接](http://www.songyuchao.com)也是使用这个插件

### 数据源构造

 如果你使用jekyll作为静态页面生成器可以如下构造XML

    <?xml version="1.0" encoding="UTF-8"?>
    <blogs>
    {% for post in site.posts %}
    <blog>
      <title>{{ post.title | xml_escape}}</title>
      <content>{{ post.content | xml_escape  }}</content>
      <url>http://www.site_ur.com{{ post.url }}</url>
      <time>{{ post.date | date: "%Y-%m-%d" }}</time>
    </blog>
      {% endfor %}
    </blogs>

 如果你是手动构建xml可以这样做

     <?xml version="1.0" encoding="UTF-8"?>
     <blogs>
     <blog>
       <title>这篇文章标题</title>
       <content>这篇文章的内容</content>
       <url>http://wwww.site_url.com/xxxx.html</url>
       <time>2014-2-3</time>
     </blog>
      <blog>
            <title>这篇文章标题</title>
            <content>这篇文章的内容</content>
            <url>http://wwww.site_url.com/xxxx.html</url>
            <time>2014-2-3</time>
          </blog>
     </blogs>

### 给搜索表单绑定事件

直接载入jquery.site-search.js文件，但是注意使用本插件先要载入jquery文件，载入后我们现在给搜素表单绑定我们的事件，如demo所示

     $("#search_form").siteSearch(Setting)

#### 关于Setting配置说明

在传入的Setting,必须为对象，如我在demo中

*  reviewCallback 重新渲染的页面的回调函数产，传入的参数为成功匹配的object的数组可以遍历得到每个obj，每个obj中属性有
    1. obj.url 页面的地址
    2. obj.title 页面的标题
    3. obj.content 页面内容
    4. obj.time 页面创建时间
* 如果没有回调程序将返回这个数组

### 增加搜索框

增加的搜索框有且只有一个输入框，并且有提交按钮，如下所示

    <form  role="search" id="search_form" data-url="http://www.songyuchao.com/search.xml">
        <div class="form-group">
            <input type="text"  placeholder="请输入搜索关键字" >
        </div>
        <button type="submit"  id="search_submit">搜一下</button>
    </form>