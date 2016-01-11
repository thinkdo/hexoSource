title: Html5
date: 2015-07-01 15:02:34
tags:
---
#### 一、新增标签
1、 结构标签：div的进化
  section，页面中一块内容区块，比如章节、页眉、页脚或页面的其他部分。和h1、h2等等结合使用
  article，特殊的独立区块，比如一篇文章
  aside，article内容之外，与article内容相关的辅助信息
  header，标识页面中一个内容的头部信息
  hgroup，header的补充内容
  footer，页面底部信息，脚注信息
  nav，表示导航链接的部分
  figure，文档主体内容中的一块独立的单元
2、 媒体标签：将媒体作为标签提取出来
  video，视频
  audio，音频
  embed，用来嵌入各种媒体，格式可以是Midi，Wav等等
3、 表单标签
4、 其他新增标签
  mark，标注某文字
  progress，进度条
  time，标注时间，搜索引擎用这个标签去搜索内容
  ruby，对某文字进行注释
  wbr，软换行，即自动换行
  canvas，图形绘制标签，和javascript配合使用
  details，自动“展开内容”效果
  datalist，input属性list，将这个list指定一个datalist，在输入框内就可以自动获取datalist的列表内容进行提示
  keygen,对输入框内容进行加密
  output，动态对某个页面值进行计算
  menu，菜单
#### 二、删除标签
  能被css代替的标签、frame、被新标签替代的标签、浏览器不支持的标签
#### 三、新增属性
1、 表单属性
   &lt;iframe seamless&gt; seamless表示边框消失
   &lt;iframe srcdoc="hello" src="http://www.google.com"&gt; srcdoc优先级大于src，src会被srcdoc覆盖
   &lt;iframe sandbox src="http://www.google.com"&gt; sandbox表示不能提交表单，不能执行脚本，异域，不允许跳转
2、 链接属性
  &lt;script defer&gt; defer表示推迟执行
  &lt;script async&gt; async表示是异步执行
  &lt;link rel="icon" sizes="16*16"&gt; sizes指定了浏览器标签里网页图片的大小
  &lt;a media="tv" hreflang="zh" ref="external"&gt; media表示设备是何种设备，tv表示电视，handheld表示手持设备,ref="external"表示外部网址，hreflang="zh"表示中文
3、 其他属性
  &lt;html manifest=""&gt;
  &lt;meta charset=""&gt;
  &lt;base href="http://localhost/" target="_blank"&gt;
  &lt;ol start="50" reversed&gt;有序列表的reversed表示从50开始倒序展示ol下边的li
  &lt;style scoped&gt; scoped表示当前样式只针对当前标签内部有用 
#### 四、删除属性
  能被css代替属性、多余属性
#### 五、增加全局属性
1、 自定义属性： data-type
2、 隐藏属性：&lt;label hidden&gt;
3、 自动语法纠错属性：&lt;input spellcheck="true"&gt;
4、 tab顺序跳转：&lt;input tabindex="1"/&gt;&lt;input tabindex="2"/&gt;按tab键会自动按1、2的顺序进行光标定位
5、 编辑属性：&lt;table contenteditable="true"&gt;标签内容可编辑
6、 全局编辑属性：window.document.designMode="on",全体内容均可编辑
#### 六、属性值
1、&lt;meta name="viewport"/&gt;
viewport有几个属性，
a）content="width=device-width"，表示使当前页面“适应设备宽度”
b）content="user-scalable=0"，表示不允许用户手动缩放，默认值为1
c）content="initial-scale=1"，表示不对当前“适应设备宽度”的页面进行缩放，这句话的意思是initial-scale本身会将页面适应设备宽度并且针对适应后的宽度设置缩放值，如果initial-scale=2则表示宽度缩小一倍，假如原来的宽度是120px，initial-scale=2后宽度将变为60px。Android系统上initial-scale没有默认值，ios的默认值为动态的，浏览器会自动计算使页面不出现滚动条，导致整个页面缩小。我们想要使当前页面适应设备的宽度，可以使用以下两种方式达到目的：
&lt;meta name="viewport" value="width=device-width" /&gt;缺点：无法适应iphone和ipad的横屏
&lt;meta name="viewport" value="initial-scale=1" /&gt;缺点：无法适应windowphone的横屏
将两个都写上就能互补解决横屏的问题：<meta name="viewport" value="width=device-width,initial-scale=1" />










 

