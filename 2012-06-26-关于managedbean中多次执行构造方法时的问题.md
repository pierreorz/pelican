Title: 关于ManagedBean中多次执行构造方法时的问题
Date: 2012-06-26
Category: ADF
Tags: ADF

<p>有时候需要在初始化时执行一些查询，但发现会多次执行。需要在构造方法里添加一行代码避免页面点击时多次执行初始化。<br />
if (!(Boolean)ADFUtils.getBindObject("adfFacesContext.postback")) {<br />
init()；<br />
}</p>

<p>通过页面是否postback来控制只初始化一次。</p>
