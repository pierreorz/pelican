Title: javax.el.PropertyNotFoundException错误解决
Date: 2011-06-29
Category: ADF
Tags: ADF

<p>有时候明明没有什么错误，一样的代码在别人机器上跑没问题，自己机器上跑却会出现以下这样的错误：
<pre class="brush:java">javax.el.PropertyNotFoundException: Target Unreachable, identifier 'bindings' resolved to null</pre>
这样的错误会随着代码量的增加而越发频繁，是IDE的缓存的BUG，如果重启jdeveloper 还不能解决的话，把报错的那个bindings的pagedef文件改动下（加一行空格）保存，然后clean all，再重新build下，基本能够解决这个问题。</p>
