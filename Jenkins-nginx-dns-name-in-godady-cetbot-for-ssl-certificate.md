## Jenkins with nginx reverse proxy also DNS name configuration with GoDaddy domain name in amazon Linux
  -----------------------------------------------------------------------------------------------------

1. Install Jenkins 
2. Install nginx 
3. sudo mkdir -p /etc/nginx/sites-available /etc/nginx/sites-enabled
4. sudo vi /etc/nginx/nginx.conf
   
   include /etc/nginx/conf.d/*.conf;
   include /etc/nginx/sites-enabled/*;

5. sudo vi /etc/nginx/sites-available/Jenkins

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

6. sudo ln -s /etc/nginx/sites-available/jenkins /etc/nginx/sites-enabled/

7. sudo nginx -t

8. sudo systemctl restart nginx

8. we need to add Jenkins server public IP/elastic ip in godady domaine name entry like below screenshot 

## Adding ssl certificate by using  certbot in amazon linux
  --------------------------------------------------------

1. sudo dnf install -y certbot python3-certbot-nginx

2. certbot --version

3. sudo certbot --nginx -d jenkins.arjun-devops.xyz -- after executing this command it will ask email id and then it will ask proceed yes.
