# Mobile Debugging

### Routing moible device network through a computer

1. enable server on a external public port
`mate /etc/apache2/httpd.conf`
insure that Apache is allowing traffic from the outside:


    # no external access to web server
    # Listen localhost:80
    # Listen localhost:443
    
    # allow traffic from external IPs
    Listen 80
    Listen 443

    
2. restart apache. In terminal run `sudo apachectl restart`
3. install Charles Proxy http://charlesproxy.com (or any other proxy server).
4. Connect the computer to a wired connection and the wireless to the same network the mobile device is on.
5. Turn on the proxy. `proxy > proxy settings... > proxies and check enable transparent HTTP proxying`
6. on the mobile device send all traffic to the computer's proxy server. On iOS go to `settings > wifi > select your wifi and click the icon on the far right > under HTTP Proxy > click Manual > for server enter the wifi IP address of your computer (find the IP with terminal via ifconfig), for port enter 8888`
7. When the mobile device connects, Charles will pop-up a dialog to approve the device. Once approved all traffic will be through Charles Proxy.

### SSL Traffic

8. If there is HTTPS data then enable SSL proxying. `proxy > proxy settings... > ssl and check enable SSL proxying, click add and enter all the URLs in the Host field`
9. download the certificate for charles proxy to decrypt and rencrypt your traffic. On the mobile device go to http://charlesproxy.com/charles.crt and install the certificate.


### Troubleshooting

Error: "Failed to load resource: The certificate for this server is invalid. ..."  in the console log or images/code not download.
Cause: You have SSL traffic but it's not appoved. Make sure the SSL server is added to Charles Proxy under SSL proxying and that the mobile device has the certificate installed.



