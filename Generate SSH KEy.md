# OpenStack-Learn
###Generating a new SSH key and adding it to the ssh-agent
<pre>
bertopeng17@bertopeng17-ThinkPad-T520:~$<b> ssh-keygen -t rsa -b 4096 -C syaifulahdan@gmail.com</b>
Generating public/private rsa key pair.
Enter file in which to save the key (/home/bertopeng17/.ssh/id_rsa):
Enter passphrase (empty for no passphrase): <b>*********</b>
Enter same passphrase again: <b>*********</b>
Your identification has been saved in /home/bertopeng17/.ssh/id_rsa.
Your public key has been saved in /home/bertopeng17/.ssh/id_rsa.pub.
The key fingerprint is:
71:51:2b:a4:1d:b1:dd:e5:d8:6d:81:70:95:67:01:e4 syaifulahdan@gmail.com
The key's randomart image is:
+--[ RSA 4096]----+
|          =++++++|
|         + =o+ *=|
|        o = oEo.*|
|         o .   . |
|        S        |
|                 |
|                 |
|                 |
|                 |
+-----------------+
bertopeng17@bertopeng17-ThinkPad-T520:~$
</pre>

###Checking for existing SSH keys
<pre>
bertopeng17@bertopeng17-ThinkPad-T520:~$ <b>ls -al ~/.ssh</b>
total 20
drwx------  2 bertopeng17 bertopeng17 4096 Mar 17 02:34 .
drwxr-xr-x 36 bertopeng17 bertopeng17 4096 Mar 17 02:33 ..
-rw-------  1 bertopeng17 bertopeng17 3326 Mar 17 02:34 id_rsa
-rw-r--r--  1 bertopeng17 bertopeng17  748 Mar 17 02:34 id_rsa.pub
-rw-r--r--  1 bertopeng17 bertopeng17  888 Mar 17 02:07 known_hosts
bertopeng17@bertopeng17-ThinkPad-T520:~$ 
</pre>
