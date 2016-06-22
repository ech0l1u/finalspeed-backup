
<pre><code>//本宝宝Linux水平属于<strong>尚未入门</strong>，英语水平不及<strong>高中毕业</strong>
//为什么用英语写纯粹是因为输入法换来换去麻烦
//有什么说错的地方还请见谅
</code></pre>

<p><strong>finalspeed</strong> is a good program to improve performance of TCP. This is the  <a href="https://github.com/d1sm/finalspeed/" title="Title"> origin Github page</a>. I did not clone or fork the project ruslt origin source could not be shown. It's a pity that the author deleted all useful code to promte his new project <a href="http://www.xsocks.me/" title="Title">Xsocks</a>. Frankly I do not <strong>trust</strong> any project close-source although I did not have code of finalspeed. Anyhow, it <strong>was</strong> a open-source project.</p>

#Summary

<p>This is about to setup finalspeed server on Linux, client on Linux and Windows</p>

#Server

##Requirement

<p>256MB RAM recommanded(more bandwith, more RAM needed)</p>

<p>CentOS or Debian or Ubuntu</p>

<p>Server and client are both reqiured at the same time to use</p>

<pre><code>//实际上这里面所有代码都是在CentOS上用的
//All code in this md is for CentOS</code></pre>
<pre></pre>

##Installing Steps

###Before Installing(Only for some port important like your ssh port had been changed)

When Finalspeed runs iptables will be started, you have to do something to prevent something going.

####Cloes system firewall only for CentOS 7

<pre><code>systemctl stop firewalld
systemctl mask firewalld
</code></pre>

####Config iptables

<pre><code>iptables -A INPUT -p tcp --dport the_port_important -j ACCEPT
iptables -A OUTPUT -p tcp --dport the_port_important -j ACCEPT
service iptables save</code></pre>

##Install and run

###Download and run the script to install Finalspeed

<pre><code>wget https://raw.githubusercontent.com/ech0l1u/finalspeed-backup/master/install_fs.sh
chmod +x install_fs.sh
./install_fs.sh 2>&1 | tee install.log
//弄完后根目录会多一个fs的文件夹出来，里面包括fs.jar及重启，停止，开始服务的几个脚本</code></pre>

###Start

<pre><code>sh /fs/start.sh</code></pre>

###Stop

<pre><code>sh /fs/stop.sh</code></pre>

###Restart

<pre><code>sh /fs/restart.sh</code></pre>

###Uninstall and remove file

<pre><code>sh /fs/stop.sh
rm -rf /fs</code></pre>

###Check server log

<pre><code>tail -f /fs/server.log</code></pre>

##Config

###Change the port

<p>The default port on server is 150</p>

<pre><code>mkdir -p /fs/cnf/
echo new_port > /fs/cnf/listen_port
sh /fs/restart.sh</code></pre>

###Start with boot

<pre><code>vi /etc/rc.local</code></pre>

add <pre><code>sh /fs/start.sh</code></pre>
to rc.local and save.

###Restart at 3:00 am everyday

<pre><code>crontab -e</code></pre>

add <pre><code>0 3 * * * sh /fs/restart.sh</code></pre>and save.


#Complete soon












