## Jenkins with nginx reverse proxy also DNS name configuration with GoDaddy domain name in amazon Linux
  -----------------------------------------------------------------------------------------------------

1. Install Jenkins 
2. Install nginx 
3. sudo mkdir -p /etc/nginx/sites-available /etc/nginx/sites-enabled
4. sudo vi /etc/nginx/nginx.conf
```
   
   include /etc/nginx/conf.d/*.conf;
   include /etc/nginx/sites-enabled/*;

```
6. sudo vi /etc/nginx/sites-available/Jenkins

 ```
   server {
    listen 80;

    server_name jenkins.arjun-devops.xyz; # Replace with your domain

    location / {
        proxy_pass http://localhost:8080; # Jenkins runs on port 8080
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    location ~ /\. {
        deny all;
    }
}

```
```
sudo ln -s /etc/nginx/sites-available/jenkins /etc/nginx/sites-enabled/ #  nginx  nginx reverse proxy  solft link
sudo nginx -t # check syntax of nginx configuration properly configured or not
sudo systemctl restart nginx # restart nginx to reflect

 ```

8. we need to add Jenkins server public IP/elastic ip in godady domaine name entry like below screenshot 

## Adding ssl certificate by using  certbot in amazon linux
  --------------------------------------------------------
  # install cerbot and depedencies
   ```
   sudo dnf install -y certbot python3-certbot-nginx
   certbot --version
   ```
# Add dns name with certbot
  ```
  sudo certbot --nginx -d jenkins.arjun-devops.xyz

```
 # After executing above command it will ask email id and then it will ask proceed yes.
