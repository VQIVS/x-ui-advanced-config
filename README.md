## Freenet advanced config
How to use CDN and Worker and reverse-proxy

## Befor you start go back and read article below

- [freenet basic config](https://github.com/VQIVS/freenet-basics-old-panel-)


## advanced features of x-ui

- CDN
- Worker 
- revrese-proxy



## CDN
``` 
First you should create account at https://cloudflare.com

2nd add your website domain to cloudflare panel 

3rd dns zone (dns reccord) one for server panel and one for protocol conections

!!! for server dns reccord you should add a A reccord with server ip and turn off the proxy option 
 
 !! and for protocol do above with proxy option 

  ! get ssl certs for all domains you will use 
``` 
After you done the steps above you should login to your x-ui panel

## make config

![9D3620B8-04BC-4E90-9B90-779CE5E86919_1_201_a](https://user-images.githubusercontent.com/119480978/235964669-da92afde-17e1-48f8-bf5c-310e261834d7.jpeg)

```
## hints
!!! we have 6 cloudflare ports (443 , 8443 , 2053 , 2083 , 2087 , 2096 )

 !! suggested transmition methods are WS and http (not working on cloudflare only direct server)

  !for using tls option add the cert files that are generated in previous article 
  the first is ssl and the other is key 
  
```
## bind your to domain 

![696300D0-F55F-46AE-866F-07BBBCEC4A9B_1_201_a](https://user-images.githubusercontent.com/119480978/235963947-f53e481f-3449-4c61-961d-57c588a992a8.jpeg)
add your ssl and certificate path to panel config and after that you can use domain to enter x-ui

# Reverse Proxy

-----------------------------------------------------------
This is whole package for X-UI and certbot with nginx reverse proxy
---------------------------------------------------------

#0 update server
apt update && apt upgrade -y

#1 Firewall Settings
apt install ufw -y

ufw allow 22
ufw allow 80
ufw allow 443
ufw allow Port_XUi


ufw enable
ufw status

ufw disable

#2 install NGINX & Certbot
sudo apt install nginx certbot python3-certbot-nginx -y

#3 copy default NGINX config to your website
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/vpn.qivps.online

#4 enable your website 
ln -s /etc/nginx/sites-available/vpn.qivps.online/etc/nginx/sites-enabled/


cd /etc/nginx/sites-enabled && ls -la

#5 edit your website config file and edit as below
nano /etc/nginx/sites-available/vpn.qivps.online

#5.1 remove default values  
server_name my.domain.com;

#add another location

location /downloader {

        if ($http_upgrade != "websocket") {

            return 404;

        }

        location ~ /downloader/\d\d\d\d\d$ {

            if ($request_uri ~* "([^/]*$)" ) {

                set $port $1;

            }

            proxy_redirect off;

            proxy_pass http://127.0.0.1:$port/;

            proxy_http_version 1.1;

            proxy_set_header Upgrade $http_upgrade;

            proxy_set_header Connection "upgrade";

            proxy_set_header Host $host;

            proxy_set_header X-Real-IP $remote_addr;

            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

        }

        return 404;

    }
	
#5.2 restart NGINX service	
systemctl restart nginx

#6 get a free SSL 
certbot --nginx -d vpn.qivps.online --register-unsafely-without-email

#7 install xRay panel FranzKafkaYu "https://github.com/FranzKafkaYu/x-ui/blob/main/README_EN.md"
bash <(curl -Ls https://raw.githubusercontent.com/FranzKafkaYu/x-ui/master/install_en.sh)

#8 Note
if you want to use cdn, then use 127.0.0.1 in listening ip for users



