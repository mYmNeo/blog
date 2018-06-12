---
title: iptables command(docker related)
date: 2016-04-27 22:32:29
tags: 
    - linux
    - iptables
    - docker
---
+ flush all rules
{% codeblock lang:bash %}
sudo iptables -P INPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT
sudo iptables -F
sudo iptables -X
sudo iptables -t nat -F
sudo iptables -t nat -X
{% endcodeblock %}
