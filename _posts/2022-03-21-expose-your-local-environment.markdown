---
layout: post
title:  "Expose your local environment"
date:   2022-03-21 11:31:50 +0100
categories: setup
---

Exposing your local environment can be very usefull to test an API or to test your frontend on a mobile phone without publishing it. Of course on the same network you can directly target the IP adress of the PC but if your want to access vhost because your using MAMP/XAMP, you have to do some little configuration.

In this post, two methods will be explain but there are more.

## Exposing to your local network

### Prerequistes
All devices have to be connected on the same network.

### Install SquidMan

SquidMan is a proxy and it is completely free. Go to the [official website](https://squidman.net/squidman/), download the latest version and install it. 

Note: You can use any other proxy software if you prefer.

### Configure SquidMan
Run SquidMan and open the preferences settings.

To allow the access to the localhost, open the template tab and comment the line: `http_access deny to_localhost` by adding a `#` at the beginning.
If you want to access your local environment throw http comment the line: `http_access deny CONNECT !SSL_ports`

On the clients tab, add a specific IP to allow only one client to connect to your proxy such as `192.168.1.42` or add a specific subnet like `192.186.1.0/24`.

### Setting the proxy on the second device
Now on the second device, add the proxy adress to your network configuration (IP from device you want to expose locahost) and put the port of SquidMan (8080 by default).

Now you can access your vhost or directly localhost from your second device.

## Exposing to public using tunneling

To expose your local environmnent to the outside, you can create a tunnel from your device to a public domain. For this purpose, [ngrok](https://ngrok.com/) will be used. A good alternative is [localhost.run](https://localhost.run/). 

### Install and run ngrok
Go to the [official download link](https://ngrok.com/download), select your OS and just follow the steps.

If you need to rewrite the header of the request because you use a vhost (MAMP, XAMP):
```bash
$ ngrok http -host-header=rewrite yoursite.dev:80

ngrok by @inconshreveable                                                            (Ctrl+C to quit)
                                                                                                     
Session Status                online                                                                 
Account                       *** (Plan: Free)                                                
Version                       2.3.40                                                                 
Region                        United States (us)                                                     
Web Interface                 http://127.0.0.1:4040                                                  
Forwarding                    http://f7ed-146-4-127-6.ngrok.io -> http://yoursite.dev:80             
Forwarding                    https://f7ed-146-4-127-6.ngrok.io -> http://yoursite.dev:80 
```

You can now access to your local environment from any device connected to the web.


Note: ngrok offers other services but not all are free. Checkout the [documentation](https://ngrok.com/docs) for more information.