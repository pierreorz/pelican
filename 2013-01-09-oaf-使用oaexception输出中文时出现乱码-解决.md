Title: OAF 使用OAException输出中文时出现乱码 解决
Date: 2013-01-09
Category: ebs
Tags: oaf
<p>使用throw new OAException(“你们好”,OAException.WARNING);时出现乱码，尝试new String("你们好”.getBytes("GBK"),"UTF-8")依然没用。</p>

<p>检查JDEV的Preferences中ENCODING已经更改为“UTF-8”，纠结了好一阵子，才发现工程的Project Settings的Compiler里也有一个ENCODING没有改，囧改好之后再测试乱码问题即解决</p>
