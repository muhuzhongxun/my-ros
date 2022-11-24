---


---

<h1 id="rospy">rospy</h1>
<p>=&gt;<a href="http://wiki.ros.org/rospy/Overview/Initialization%20and%20Shutdown">http://wiki.ros.org/rospy/Overview/Initialization and Shutdown</a></p>
<h2 id="初始化">1.初始化</h2>
<h4 id="初始化你的ros节点">1.1 初始化你的ROS节点</h4>
<pre><code>rospy.init_node('my_node_name'[,anonymous = True])
</code></pre>
<p>rospy.init_node(name, anonymous=False, log_level=<a href="http://rospy.INFO">rospy.INFO</a>, disable_signals=False)</p>
<ul>
<li>init_node 有几个可选择的关键字，<br>
anonymous = True ， 给节点添加一个随机数。如果有两个相同名称的节点在ROS graph时，老的节点会被关闭。</li>
<li>log_level=<a href="http://rospy.INFO">rospy.INFO</a><br>
设置默认的日志级别对日志发布的消息来 <a href="http://wiki.ros.org/rosout">rosout</a> .</li>
<li>disable_signals=False<br>
默认情况下，rospy寄存器的信号处理程序，以便它可以关闭通过Ctrl+C . 在一些代码，你可能希望禁止这一点…</li>
</ul>
<h2 id="关闭">1.2 关闭</h2>
<h4 id="测试关闭">1.2.1 测试关闭</h4>
<p>最常见的测试关闭rospy的使用方法为：</p>
<pre><code>while not rospy.is_shutdown():
   do some work
</code></pre>
<p>and</p>
<pre><code>... setup callbacks
rospy.spin()
</code></pre>
<p>rospy.spin() 会执行 sleeps() 直到 is_shutdown()方法为真。它可以防止你的py函数线程退出。</p>
<h4 id="registering-shutdown-hooks">1.2.2 Registering shutdown hooks</h4>
<p>rospy.on_shutdown(h)<br>
在rospy关闭前调用h方法。保证服务、服务器完整地运行。</p>
<pre><code>def myhook():
  print "shutdown time!"
rospy.on_shutdown(myhook)
</code></pre>
<h4 id="manual-shutdown-advanced">1.2.3 Manual shutdown (Advanced)</h4>
<p>强制关闭，需要人工调用该关闭程序。</p>
<pre><code>rospy.signal_shutdown(reason)
</code></pre>
<h2 id="消息">2. 消息</h2>

