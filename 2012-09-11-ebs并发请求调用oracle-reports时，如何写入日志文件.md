Title: EBS并发请求调用Oracle reports时，如何写入日志文件
Date: 2012-09-11
Category: ebs
Tags: reports

<p>EBS并发请求调用procedure时，直接在被调用的procedure中使用fnd_file.put_line即可达到要求；</p>

<p>如果并发请求调用的是oracle reports时，写入日志文件需要使用reports的方法。</p>

<p>在Before/After report Trigger中使用SRW.message(0,'Message');</p>

<p>中断报表执行使用SRW.break;</p>

<p>&nbsp;</p>
