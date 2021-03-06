Title: 关于定制validator
Date: 2012-06-26
Category: ADF
Tags: ADF

<p>一个时刻字段，要求输入00:00-12:60这样的时刻范围<br />
使用如下的正则表达式，过滤掉了不合规则的数字之后，还差一个逻辑，结束时刻不能小于开始时刻，比如：10：00-9：00这样的输入也是不合法的。正则太折磨眼力了，应该也是可以做到这点的吧，为了偷懒，就定制个validator来处理这个点。
<div>
<blockquote>&lt;af:validateRegExp pattern="([0-1][0-9]|2[0-4])\:([0-5][0-9]|60)\-([0-1][0-9]|2[0-4])\:([0-5][0-9]|60)" messageDetailNoMatch="请输入时刻，例如 00：00-24：60 " hint="请输入时刻，例如 00：00-24：60"/&gt;</blockquote>
</div>
<strong>Step1</strong>。创建一个<strong>ValidatorTime</strong>类实现Validator接口
<div>
<blockquote>package com.adfkf.validators;</blockquote></div></p>

<p>import javax.faces.application.FacesMessage;<br />
import javax.faces.component.UIComponent;<br />
import javax.faces.component.UIInput;<br />
import javax.faces.context.FacesContext;<br />
import javax.faces.validator.Validator;<br />
import javax.faces.validator.ValidatorException;</p>

<p>import org.apache.myfaces.trinidad.component.UIXInput;</p>

<p>public class ValidatorTime implements Validator {<br />
public ValidatorTime() {<br />
super();<br />
}</p>

<p>public void validate(FacesContext facesContext, UIComponent uiComponent,<br />
Object object) {</p>

<p>String value = null;<br />
String a, b, c, d = null;<br />
Boolean bool = false;<br />
if ((facesContext == null) || (uiComponent == null)) {<br />
throw new NullPointerException();<br />
}
if (!(uiComponent instanceof UIXInput)) {<br />
return;<br />
}
if (null == object) {<br />
return;<br />
}
//12:00-23:00<br />
value = object.toString();<br />
if (value != null &amp;&amp; value.length() == 11) {<br />
a = value.substring(0, 2);<br />
b = value.substring(3, 5);<br />
c = value.substring(6, 8);<br />
d = value.substring(9, 11);<br />
try {<br />
Integer intA = Integer.valueOf(a);<br />
Integer intB = Integer.valueOf(b);<br />
Integer intC = Integer.valueOf(c);<br />
Integer intD = Integer.valueOf(d);<br />
if (intC &gt; intA || (intA == intC &amp;&amp; intD &gt; intB)) {<br />
bool = true;<br />
} else {<br />
bool = false;<br />
}</p>

<p>} catch (Exception e) {<br />
bool = false;<br />
}</p>

<p>}<br />
if (!bool) {<br />
FacesMessage message = new FacesMessage();<br />
message.setDetail("开始时刻大于结束时间");<br />
message.setSummary("时刻输入有误");<br />
message.setSeverity(FacesMessage.SEVERITY_ERROR);<br />
throw new ValidatorException(message);</p>

<p>}</p>

<p>}<br />
}

<strong>Step2 </strong>在faces-config.xml中注册这个validator
<div>
<blockquote>&lt;validator&gt;<br />
&lt;validator-id&gt;validateTime&lt;/validator-id&gt;<br />
&lt;validator-class&gt;com.adfkf.validators.ValidatorTime&lt;/validator-class&gt;<br />
&lt;/validator&gt;</blockquote>
</div>
<strong>Step3 </strong>页面中使用定制的validator
<div>
<blockquote>&lt;af:inputText value="#{row.bindings.ReimTime.inputValue}" disabled="#{sessionScope.flag}"<br />
label="#{bindings.CostDetailVO.hints.ReimTime.label}"<br />
required="#{bindings.CostDetailVO.hints.ReimTime.mandatory}"<br />
shortDesc="#{bindings.CostDetailVO.hints.ReimTime.tooltip}"<br />
id="id2"&gt;<br />
&lt;af:validateRegExp pattern="([0-1][0-9]|2[0-4])\:([0-5][0-9]|60)\-([0-1][0-9]|2[0-4])\:([0-5][0-9]|60)" messageDetailNoMatch="请输入时刻，例如 00：00-24：60 " hint="请输入时刻，例如 00：00-24：60"/&gt;<br />
&lt;f:validator validatorId="validateTime"/&gt;<br />
&lt;/af:inputText&gt;</blockquote>
</div>

