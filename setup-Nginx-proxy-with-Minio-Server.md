# Setup Nginx proxy with Minio Server

Nginx is an open source Web server and a reverse proxy server.  

In this recipe we will learn how to set up Nginx proxy with Minio Server. 

## 1. Prerequisites
Install Minio Server from [here](http://docs.minio.io/docs/minio).

## 2. Installation
Install Nginx from [here](http://nginx.org/en/download.html).  

## 3. Configuration
Add  below content as a file ``/etc/nginx/sites-enabled``  and also remove the existing ``default`` file in same directory.
```
server {
 listen 80;
 server_name example.com;
 location / {
   proxy_set_header Host $host;
   proxy_set_header X-Real-IP $remote_addr;
   proxy_set_header X-Forwarded-Proto $scheme;
   proxy_pass http://localhost:9000;
 }
}
```
Note: 
* Replace example.com with your own hostname.
* Replace ``http://localhost:9000``  with your own server name.

## 4. Recipe Steps
### Step 1: Start Minio server. 

```
$ minio server /mydatadir
```

### Step 2: Restart Nginx server.
```
$ sudo service nginx restart
```
