Title: 如何在MB中对selectionListener collectionModel.makeCurrent调用
Date: 2012-06-26
Category: ADF
Tags: ADF
<p>如何在MB中对Table的默认"#{bindings.PromotionVO1.collectionModel.makeCurrent}"进行调用？</p>

<p>当需要重写adf:table的缺省的selectListener时，可以在自己绑定的MB的方法里，调用默认的makeCurrent方法。取得当前行的数据，进行自己的定制操作。方法如下：
<div>
<blockquote>//调用缺省makeCurrent<br />
JSFUtils.resolveMethodExpression("#{bindings.yourVO.collectionModel.makeCurrent}",<br />
new Class[] { SelectionEvent.class },<br />
new Object[] { selectionEvent });</blockquote>
</div>
取得选中行的数据
<div>
<blockquote>Row selectedRow =<br />
(Row)JSFUtils.resolveExpression("#{bindings.yourVOIterator.currentRow}");</blockquote>
</div>
然后就可以针对取得的数据进行定制开发了。</p>
