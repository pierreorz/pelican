Title: 如何让af:inputListOfValues（LOV）的初始值显示为Blank而不是默认的VO的First Row
Date: 2011-07-20
Category: ADF
Tags: ADF

<p>目前LOV控件在页面初始化时默认显示的是第一条记录，如果想让LOV初始化的时候不显示记录应该如何设置呢？</p>

<p>方法一. 通过在BackingBean的构造函数里设置LOV的值为空字符串这种做法基本可以达到需求。但总感觉这种方法很别扭，走了弯路。</p>

<p>本文介绍另外一种更为简单的方法。通过EL表达式实现需求。
<pre class="brush:java">           &lt;af:inputListOfValues id="ilov1"
                                    popupTitle="Search and Select: #{bindings.CodeType.hints.label}"
                                    value="#{adfFacesContext.postback == false ? bindings.CodeType.nullValueString : bindings.CodeType.inputValue}"
                                    label="#{bindings.CodeType.hints.label}"
                                    model="#{bindings.CodeType.listOfValuesModel}"
                                    required="#{bindings.CodeType.hints.mandatory}"
                                    columns="#{bindings.CodeType.hints.displayWidth}"
                                    shortDesc="#{bindings.CodeType.hints.tooltip}"
                                    binding="#{backing_pages_frs001.ilov1}"
                                    valueChangeListener="#{backing_pages_frs001.valueChange}"
                                    &gt;</pre>
看这段代码：
<blockquote>
<pre>value="#{<span style="color: #ff0000;">adfFacesContext.postback == false ? bindings.CodeType.nullValueString : </span>bindings.CodeType.inputValue}"</pre>
</blockquote>
当页面没有postback的时候，给LOV字段的值设为<strong>nullValueString</strong>，即可。</p>

<p>今天太困了。。。先睡了。。。不贴图了~</p>
