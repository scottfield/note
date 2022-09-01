###Firewall
```
# firewall-cmd --permanent --add-port=100/tcp
# firewall-cmd --permanent --add-port=200-300/tcp
firewall-cmd --permanent --add-service=http
# firewall-cmd --reload
# firewall-cmd --list-ports
# firewall-cmd --list-services
```