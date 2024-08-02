# GeoIP2Fast Server

![](https://raw.githubusercontent.com/rabuchaim/geoip2fastserver/main/geoip2fastserver01.png)

![](https://raw.githubusercontent.com/rabuchaim/geoip2fastserver/main/geoip2fastserver02.png)

## Features
- Lightweight and super fast
- You can use our geoip2 data files based on Maxmind Geolite2 CSV files or any MMDB file (We take care of all exceptions and handle all reserved networks before sending data to the user. The user will always receive a ready-to-use response)
- Fully customizable, from the server name that appears in the http header to the last character of the response sent to the user
- Ratelimit and Firewall with a decision time lower than 0.000005 second. It doesn't analyze just 1 second, you can configure to block by 12 seconds any IP that do 87 requests in 4 seconds. 
- An elegant and dynamic firewall that lets you control which public IPs you want to allow on your server. This server was not designed to be face on internet, but I know that one day someone will do that... so the application is ready to deal with suffering in silence.
- Tested against DoS attacks and buffer overflows. On a local network, it can work with a timeout of 0.3 seconds and does not receive more than 64 bytes per request
- It can be behind a load balancer/proxy. It detects the x-forwarded-for and x-real-ip headers and works with them if applicable. You can control access via x-forwarded-host if you want.
- And if it can be behind a load balancer, it has to have a decent health-check. And you can remove the server from the loadbalancer without having to touch the loadbalancer or stop the service by taking down its users. Just "touch" a file called "stop_hc" in the application directory and it starts returning 404 in /geoip/hc calls, and then just wait for the loadbalancer to smoothly stop sending requests to your instance. You can configure the location and name of this file as well.
- A self-explanatory API:
  - GET /geoip/1.1.1.1
  - GET /geoip/1.1.1.1/pretty
  - GET /geoip/1.1.1.1/csv
  - GET /geoip/hc
- No memory leak. We have been testing for 5 days with all IPs on the internet and memory usage remains the same.
- There is docker available too. You can create containers with 50Mb of RAM, 100M, 150M or 550M, depending on the database you want to use. Works with IPv4 and IPv6.
- You can individually disable any check to make it a little faster, it reloads the configurations without restarting, sends it via syslog, you can send logs to Mars by configuring just one line and many other flowers. It just doesn't make coffee and answer the doorbell.
