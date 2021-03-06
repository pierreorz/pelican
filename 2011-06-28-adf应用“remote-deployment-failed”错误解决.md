Title: ADF应用“Remote deployment failed”错误解决
Date: 2011-06-28
Category: ADF
Tags: ADF

<p>ADF应用debug模式下最常出现的问题就是远程发布失败了。控制台打印的错误信息如下：
<pre class="brush:plain">[07:21:55 PM] ####  Deployment incomplete.  ####
[07:21:55 PM] Remote deployment failed (oracle.jdevimpl.deploy.common.Jsr88RemoteDeployer)
#### Cannot run application XXX due to error deploying to IntegratedWebLogicServer.
[Application XXX stopped and undeployed from Server Instance IntegratedWebLogicServer]
&lt;Logger&gt;&lt;error&gt; ServletContainerAdapter manager not initialized correctly.</pre>
解决方法有两种：</p>

<p>方法一：进入weblogic控制台<span style="color: #0000ff;">http://127.0.0.1:7101/console</span>
<pre class="brush:plain">用户名：weblogic
密 码：weblogic1</pre>
此时控制面板的左上区域应该会有两个按钮“<span style="color: #0000ff;">激活更改</span>”，“<span style="color: #0000ff;">撤销所有更改</span>”，点击任一按钮皆可，然后重新debug，问题解决。</p>

<p>方法二：查看控制台信息，找到类似于“<span style="color: #0000ff;">C:\Documents and Settings\Administrator\Application Data\JDeveloper\system11.1.1.3.37.56.60\o.j2ee\drs\</span>”的路径（这个路径跟你jdeveloper安装路径相关，system目录后的数字也是不同的）。进入到drs目录下，清空所有内容。重新debug，问题解决。<!--more--></p>
