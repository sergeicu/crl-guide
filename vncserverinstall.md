
### Installing and running VNCserver 

To setup VNCserver you need to 

A. install VNC Viewer on your laptop. 

B. install VNCserver on your BCH machine  

C. Start vncserver 

For A - download the binary from public website - search for `realvnc` or `tigervnc` on google. 

For B - you can try to install vncserver yourself via `yum` or `snap` on your BCH machine. 

e.g. `sudo yum install tigervnc-server​` 

I personally had some trouble here and had to ask Sean for help because my machine had some miscalibrations of GPL libraries. 

For C - as long your BCH machine has not been restarted - you will need to run `vncserver` _only once_ in the terminal of your BCH machine

On your BCH machine terminal: 

$ vncserver >> to initialize vncserver after restart or to start it for the first time 

$ vncserver -list >> to view list of currently running sessions  

$ vncserver -kill &lt;sessionID> >> to kill any running session 

How to setup VNCviewer on your laptop: 

1. Start VNCviewer on your laptop, click New Connection

2. ssh into your BCH machine via terminal and get the exposed DNS server address like this - 

$ nslookup &lt;youBCHmachinename> 

>> for me this command yields: 

 >> Non-authoritative answer: 

 >> Name: rayan.tch.harvard.edu 

 >> Address: _10.16.6.179  _

3. Add VNCserver like this ->  `&lt;DNS_ip_address>:**590**&lt;sessionID>` 

e.g. 10.16.6.179:5901

Note that the green section would be different for your own machine. 590 is the standard port. &lt;sessionID> will be different for you (you can get it from `vncserver -list` command)

4. Add name for your connection. Click ok. 

5. You can repeat this process again for other machines if necessary. e.g. if you SSH into other machines at CRL you can run vnc there also (as long as it is installed) 
