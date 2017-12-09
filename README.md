## mescroll官网 : http://www.mescroll.com/
## mescroll文档 : https://github.com/mescroll/mescroll.git
<br/>
<br/>

## mescroll所有版本:
<br/>

### v 1.2.8.1 --- 2017-12-10

1. 新增<a href="http://www.mescroll.com/preview.html?name=search">关键词搜索案例  mescroll-search</a>  

2. up的toTop新增html的配置(回到顶部按钮)  具体运用可查看<a href="http://www.mescroll.com/preview.html?name=search">关键词搜索案例  mescroll-search</a>  
<br/>
<br/>

### v 1.2.8 --- 2017-12-08

##### 一. 新增内容: 

1. 回到顶部按钮可配置添加在指定div. (初始化mescroll时,在 up 配置 toTop的 warpId 即可)  . <a href="http://www.mescroll.com/api.html#options">详见官方文档说明</a>  

2. 新增 <b>mescroll.getStep</b> 计步器, 可用于模拟帧动画. <a href="http://www.mescroll.com/api.html#others">详见官方文档说明</a>  

3. 新增<a href="http://www.mescroll.com/preview.html?name=swiper-tap">轮播菜单案例  mescroll-swiper-tap</a>  

4. 新增<a href="http://www.mescroll.com/preview.html?name=swiper-nav">轮播导航案例 mescroll-swiper-nav</a>  

5. 新增<a href="http://www.mescroll.com/preview.html?name=sticky">吸顶悬浮案例 mescroll-sticky</a>  
<br/>

##### 二.优化代码:
1. 集中处理常见异常的提示  
2. 简化内部dom操作逻辑  
<br/>

##### 三.修复bug:  
1. 修复移动端系统停止跟踪触摸事件时,未能及时结束下拉刷新的问题
2. 修复调用mescroll.destroy(),未移除回到顶部按钮的问题
3. 修复配置up不使用,可能会输出错误日志的问题

<br/>
<br/>

### v 1.2.5 --- 2017-11-25

##### 一. 新增方法: 

1. <b>mescroll.setPageNum(num)</b> : 设置当前page.num的值  

2. <b>mescroll.setPageSize(size)</b> : 设置当前page.size的值  

3. 获取系统平台 mescroll.os<br/>
	<b>mescroll.os.ios</b> 为true, 则是ios设备;<br/>
	<b> mescroll.os.android</b> 为true, 则是android设备;<br/>
	<b> mescroll.os.pc</b> 为true, 则是PC端;<br/>
<br/>

##### 二.优化代码:
1. 结束上拉和下拉状态时,取消进度条的动画,减少资源消耗  

2. 取消mustToTop无意义的配置  

3. 加入常见错误log提示  

4. 调整up配置auto的逻辑,避免初始化时可能会触发两次upCallback的问题  
<br/>

##### 三.修复重要bug:  

Q. 在iOS的微信,QQ,Safari等浏览器,列表顶部下拉和底部上拉露出浏览器灰色背景,卡顿2秒,不满屏下拉刷新dom元素可能不渲染 ?  

A. 这个问题只存在iOS浏览器; android,PC是正常的; 原因是iOS自身的回弹效果导致的, 解决方法如下:  

1. mescroll.min.css和mescroll.min.js更新到1.2.5版本  

2. 在"mescroll"的div 加入 "mescroll-bounce"子div, 必须结构如下: 
```
<div id="mescroll" class="mescroll">
	<div class="mescroll-bounce">

		//列表内容,如:<ul>列表数据</ul> ...
		
	</div>
</div>
```

3 . 加入mescroll-bounce的div之后,会禁止ios的webview的touchmove事件,从而阻止iOS的回弹效果.  
此时除了mescroll的div可以滑动,其他的区域匀无法滑动;    
如果你希望mescroll之外的某个div可以滑动,则可为这个div加入<b>mescroll-touch</b>的样式即可; 
 
比如你希望顶部导航菜单class="nav-top"的div可接收touchmove事件, 则class="nav-top mescroll-touch"   
如果添加<b>mescroll-touch-x</b> 则可水平滑动  ; 如果添加 <b>mescroll-touch-y</b> 则可上下滑动

mescroll-bounce的作用只在iOS生效,不必担心会影响到android和pc端的运行效果;   
mescroll-bounce的结构是固定的,所以您如果用了body为滚动区域,则要更改为div方式了.

<br/>
<br/>

### v 1.2.3 --- 2017-10-17
1.修复在某些预加载的情况下无法下拉的异常;<br/><br/>
2.调整mescroll.scrollTo(y, t)方法:<br/>
 y=0,则回到顶部; 如果要滚动到底部可以传一个较大的值,比如99999;<br/>
 t时长,单位ms,不传,则默认300; <b>如果不需要动画缓冲效果,则传0<b/>;<br/>
<br/>
<br/>

### v 1.2.1 --- 2017-10-10 

##### 一.新增配置:  

1.down的配置新增bottomOffset : 当手指touchmove位置在距离body底部20px范围内的时候结束上拉刷新,避免Webview嵌套导致touchend事件不执行  
  
  
2.up的配置新增onScroll : function(mescroll, y, isUp){ }; //y为列表当前滚动条的位置; isUp=true向上滑,isUp=false向下滑  
  
  
##### 二.调整mescroll.endSuccess  
联网成功的回调,隐藏下拉刷新和上拉加载的状态;  
mescroll会根据传的参数,自动判断列表如果无任何数据,则提示空;列表无下一页数据,则提示无更多数据;

//方法1: 后台接口有返回列表的总页数 totalPage  
mescroll.endByPage(curPageData.length, totalPage); //必传参数(当前页的数据个数, 总页数)

//方法2: 后台接口有返回列表的总数据量 totalSize  
mescroll.endBySize(curPageData.length, totalSize); //必传参数(当前页的数据个数, 总数据量)

//方法3: 您有其他方式知道是否有下一页 hasNext  
mescroll.endSuccess(curPageData.length, hasNext); //必传参数(当前页的数据个数, 是否有下一页true/false)

//方法4 (不推荐),会存在一个小问题:比如列表共有20条数据,每页加载10条,共2页.  
//如果只根据当前页的数据个数判断,则需翻到第三页才会知道无更多数据,如果传了hasNext,则翻到第二页即可显示无更多数据.  
mescroll.endSuccess(curPageData.length); //1.2.0以前版本用的都是这个方法,存在上述小问题,请升级到1.2.1吧		


##### 三.新增方法:  
					
1.销毁mescroll   
mescroll.destroy();  

2.获取滚动条的位置y  
var y = mescroll.getScrollTop();  

3.获取body的高度  
var h = mescroll.getBodyHeight();

4.获取滚动容器的高度  
var h= mescroll.getClientHeight();

5.获取滚动内容的高度  
var h= mescroll.getScrollHeight();


##### 四.其他
1.初始化mescroll检查AMD,CMD,Node环境  

2.不启用上拉,则不配置up即可,无需像以前版本必须配置 up:{use:false}  

3.优化硬件加速的逻辑,修复iOS下拉刷新有时闪白屏或者抖动的问题  

4.body默认高度100%,并且可配置body为滚动区域,简化mescroll初始化的写法.  
参考案例: http://www.mescroll.com/preview.html?name=list-mescroll-body
<br/>
<br/>

### v 1.2.0 --- 2017-10-02 
### v 1.1.8 --- 2017-09-16 
### v 1.1.7 --- 2017-09-01 
个人内测版,略过~
<br/>
<br/>

### v 1.1.6 --- 2017-08-27
down的配置新增 minAngle : 触发下拉最少要偏移的角度(滑动的轨迹与水平线的锐角值),取值区间  [0,90];<br/>
默认45度,即向下滑动的角度大于45度(方位角为45°-145°及225°-315°)则触发下拉;而小于45度,将不触发下拉,避免与左右滑动的轮播等组件冲突;<br/>
注意:没有必要配置超出[0,90]区间的值,否则角度限制无效; 因为假设配置60, 生效的方位角就已经是60°到120° 和 240°到300°的范围
<br/>
<br/>

### v 1.1.5 --- 2017-08-15 
1.取消down.resetShowDownScroll的配置项,少用且不易理解,取而代之的方法是mescroll.resetUpScroll(true);<br/>
2.简化mescroll.resetUpScroll(isShowLoading)重置列表的用法, 参数isShowLoading: 是否显示进度布局<br/>
  &nbsp;&nbsp; 2.1  默认null,不传参,则显示上拉加载的进度布局;<br/>
  &nbsp;&nbsp; 2.2  传参true, 则显示下拉刷新的进度布局 (等同于旧版本的down.resetShowDownScroll:true);<br/>
  &nbsp;&nbsp; 2.3  传参false, 则不显示上拉和下拉的进度 (常用于静默更新列表数据);
<br/>
<br/>

### v 1.1.4 --- 2017-08-10 
个人内测版,略过~
<br/>
<br/>

### v 1.1.3 --- 2017-08-06 
1.mescroll.endErr() 默认隐藏上拉加载中的布局<br/>
2.mescroll.resetUpScroll() 内部重置时间为null,而非原来的空串
<br/>
<br/>

### v 1.1.2 --- 2017-08-01 
1.PC端可自定义滚动条样式<br/>
2.可配置onScroll来监听滚动条的位置<br/>
3.主动触发下拉刷新mescroll.triggerDownScroll()显示下拉布局加入动画效果过渡<br/>
4.重置列表mescroll.resetUpScroll(isShowLoading)新加isShowLoading参数: 是否显示下拉或者上拉的进度布局<br/>
  &nbsp;&nbsp; 4.1 不传参或true,则显示进度布局;<br/>
  &nbsp;&nbsp; 4.2 传false,则不显示;常用于切换菜单时静默更新列表数据;
<br/>
<br/>

### v 1.1.1 --- 2017-07-15  
经过大半年的实践优化, 分享给大家的第一个稳定版本  
<br/>
<br/>

### v 1.0.0 --- 2016-10-10  
个人项目中使用