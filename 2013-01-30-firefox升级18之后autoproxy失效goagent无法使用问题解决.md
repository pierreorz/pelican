Title: firefox升级18之后,autoproxy失效,goagent无法使用问题解决
Date: 2013-01-30
Category: others
Tags: firefox, goagent

<p>之前使用的是17版本的firefox，配置好了autoproxy使用goagent能够正常代理，之后升级firefox18之后，却代理不了了。重装过firefox,重装过goagent，重装过autoproxy都无效。</p>

<p>试过使用IE，设置代理127.0.0.1:8087+goagent可以正常代理，因此排除goagent问题。</p>

<p>后来查看firefox18的版本说明，才发现由于安全性禁用了部分功能猜测可能由此导致无法代理</p>

<p>firefox说明：
<blockquote>禁用不安全内容：Firefox 可以禁用HTTPS安全网页中的不安全内容，来维护用户在互联网通信中的隐私。目前可以在about:config中启用这个特性。</blockquote>
打开about:config，过滤栏输入：proxy  修改如下选项</p>

<p>extensions.autoproxy.proxyMode   <strong>auto</strong>
network.proxy.type               <strong>1</strong>
signon.autologin.proxy           <strong>true</strong>
即可解决问题。</p>

<p>&nbsp;</p>

<p>&nbsp;</p>
