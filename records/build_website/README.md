## 使用 AWS lightsail 建置個人網站
- 由於已經在本機透過docker寫好網站，只需要將 code 和 database schema 放到網站上去
- 基本上透過官方文件就可以將網站設定完成

### Tech
- Laravel
- MySql
- AWS LAMP (PHP7)

### Environment
- Apache
   依照官方文件調整 apache configuration
   
- phpMyAdmin
    ``` bash
    1. download {name}.pem key (透過console下載)
    2. chmod 600 {name}.pem
    3. ssh -N -L 8888:127.0.0.1:80 -i {name}.pem bitnami@{server-ip}
    4. 貼上 http://127.0.0.1:8888/phpmyadmin 就會看到畫面摟
    5. migrate database schema
    ```

- Laravel
    - 下載相依套件 
        ``` php
        1. 進入 lightsail instance的terminal
        2. git clone 專案
        3. 執行 composer install
        4. 執行 composer update (optional)
        ```

   - .env檔建立
        ```
        Laravel key generate
        填上 DB password   
        ```

### Point domain to lightsail
- Networking 
  - Create and assign a Static IP address to an instance

- Domain & DNS
  - create a DNS zone
  - 把 Name servers 資訊貼到購買網址的後台
  - create DNS records & SSL憑證
    - 參考這部影片： https://www.youtube.com/watch?v=LDVQhN7zJvQ
   
- Renew The Let’s Encrypt Certificate
   ``` bash
   sudo /opt/bitnami/ctlscript.sh stop
   sudo /opt/bitnami/letsencrypt/lego --tls --email="{e-mail}" --domains="{domain}" --path="/opt/bitnami/letsencrypt" renew --days 90
   sudo /opt/bitnami/ctlscript.sh start
   ```
  
### Trouble Shooting
- Laravel遇到權限上的問題\
https://stackoverflow.com/questions/72877284/laravel-docker-permission-denied-the-exception-occurred-while-attempting-to-log

### Reference
- https://docs.bitnami.com/aws/infrastructure/lamp/get-started/use-laravel \
- https://docs.bitnami.com/general/how-to/understand-bncert/#certificates-not-renewed-automatically

