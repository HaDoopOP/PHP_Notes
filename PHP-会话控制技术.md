web是通过HTTP协议来实现的，HTTP是一中无状态协议，不会记录两者间的状态。
如果一个用户对网站同时请求两次，http会认为是两个不同的请求，没有来自同一个用户。独立的。

如果用户登陆了，HTTP本身不会认为你已经登陆了。再干事还需要你输入用户名密码。不能在不同页面对用户的状态进行跟踪和保存。

所以会话控制技术，就是为了对客户端进行连续的跟踪。

1.用GET
信息不安全，都暴露在URl地址上面了。

2. cookie
一中由服务器发送给客户端，存在浏览器里的一个文件。包含了客户端的一些片段信息。
setcookie（）写；$_COOKIE去拿，⚠️是只读的，不可以用什么unset去更改；

如果要删，直接在过去日期里面，调用当前时间，再减一就行了。

对网站开发人员来说，cookie存在客户端，不在服务端。不会浪费服务器资源。
但是一旦某些软件，在客户端禁止了用户使用cookie，我们先前的架构就不能用了。

3. session

是把记录存在服务端。没有脱离cookie，而是基于cookie；

cookie里面存的是session ID，如果cookie被禁止，拿url传session ID就可以了。
sessionID对应到了服务器端的session文件信息。

session_start() -->然后去操作$_SESSION就行了。

session.save_handler()很有意思，可以设置把session存到哪，比如redis，mysql....

session优点是信息安全，数据库比client一般防护的更好。

分布式服务器的时候，session扔到redis上面去。不管哪台服务器，先去redis调用信息；
session是基于cookie，cookie里存sessionID。再对应到服务器去拿状态。
SID = session_name() . '=' . session_id() SID是一个常量。当cookie被禁止的时候，可以直接传这个常量到下一个页面。
SID⚠️⚠️非常智能，当cookie开启的时候，它是空。只有当cookie被禁用的时候，它才会作用出来。不会造成又可以在cookie里面读，又通过url传的浪费。

Sesion以文件形式储存很容易造成不统一，比如在webservice1上面输入了密码，然后跳转到2了。找不到sessionID对应的文件，因为都存在服务器一上面了。
可以把session存到mem cache里面去，redis甚至于mysql。

![题目](/image/session.png)

