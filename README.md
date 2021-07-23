Adding a new client project to the server:
  1. open /etc/nginx/sites-available/default
  2. find the last project and copy / paste the code block on a new line
    example code block: 
    ```   location /needleman/ {
        proxy_http_version 1.1;
        proxy_cache_bypass $http_upgrade;

        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        proxy_cache_bypass $http_upgrade;

        proxy_pass http://localhost:8099;
      }```
  3. update the port to the next available port - http://localhost:8099 becomes http://localhost:8100
  4. save the file
  5. in the terminal run : sudo nginx -t
  6. you should see this response : 
    nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
    nginx: configuration file /etc/nginx/nginx.conf test is successful
  7. then run sudo systemctl restart nginx
