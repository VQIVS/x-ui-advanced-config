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


