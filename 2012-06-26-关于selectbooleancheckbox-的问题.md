Title: 关于selectBooleanCheckbox 的问题
Date: 2012-06-26
Category: ADF
Tags: ADF

<p>页面的 selectBooleanCheckbox 选择后，总提示 不是数字（组件value是 true 或 false,数据库存的是Number），怎么解决</p>

<p>方案有三个<br />
1。如果是基于表的Number字段(假设字段名是Flag，值是1或者0），想生成selectBooleanCheckbox ，可以重写这个VO的的 setFlag()跟getFlag()方法如下：<br />
public void setFlag(Boolean value){<br />
this.flag=value==true?1:0;<br />
}
public Boolean getFlag(){<br />
return this.flag==0?false:true;<br />
}</p>

<p>2。设置valueChangeListener.<br />
在valueChange方法里捕获当前selectBooleanCheckbox 的值，然后转化成Number类型的传给VO</p>

<p>3。如果是只读的表，可以在UI上通过EL表达式处理。</p>
