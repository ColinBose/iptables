#!/bin/bash
iptables -F
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP
#iptables -P INPUT ACCEPT
#iptables -P OUTPUT ACCEPT
#iptables -P FORWARD ACCEPT
#iptables -A OUTPUT -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT
#iptables -A INPUT -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT
#iptables -A OUTPUT -p tcp --sport 80 -m state --state ESTABLISHED -j ACCEPT
#iptables -A INPUT -p tcp --sport 80 -m state --state ESTABLISHED -j ACCEPT
#PORT 0
iptables -A INPUT -p tcp --sport 0 -j DROP
iptables -A INPUT -p tcp --dport 0 -j DROP
iptables -A OUTPUT -p tcp --dport 0 -j DROP
iptables -A INPUT -p udp --destination-port 0 -j DROP
iptables -A OUTPUT -p udp --dport 0 -j DROP
#HTTP
#iptables -A INPUT -p tcp --sport 0:1023 --dport 80 -j DROP
iptables -A INPUT -p tcp --dport 80 --sport 1024: -j ACCEPT
iptables -A INPUT -p tcp --sport 80  -j ACCEPT
iptables -A OUTPUT -p tcp --sport 80 -j ACCEPT
iptables -A OUTPUT -p tcp --dport 80  -j ACCEPT
#HTTP SECURE
iptables -A INPUT -p tcp --dport 443  -j ACCEPT
iptables -A INPUT -p tcp --sport 443  -j ACCEPT
iptables -A OUTPUT -p tcp --sport 443 -j ACCEPT
iptables -A OUTPUT -p tcp --dport 443  -j ACCEPT

#SSH
iptables -A OUTPUT -p tcp --sport 22 -j ACCEPT
iptables -A INPUT -p tcp --dport 22  -j ACCEPT

#DHCP
iptables -A INPUT -p udp --dport 67:68 --sport 67:68 -j ACCEPT

#DHS
iptables -A OUTPUT -p udp -d 142.232.191.38 --dport 53 -m state --state NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp -d 142.232.191.38 --dport 53 -m state --state NEW,ESTABLISHED -j ACCEPT
iptables -A INPUT -p tcp -s 142.232.191.38 --sport 53 -m state --state ESTABLISHED -j ACCEPT
iptables -A INPUT  -p udp -s 142.232.191.38 --sport 53 -m state --state ESTABLISHED     -j ACCEPT


#dns ip 142.232.191.38
