# Basic Nginx Deployment

#### Description:

- Create an EC2 server.
- Install Nginx in it.
- Create a sample index.html page and deploy it on that Nginx server.
- Create an elastic IP and attach it to the ec2 instance.
- Configure domain and apply SSL.
- Configure automation script for SSL renewal.

#### Create an EC2 server
 #### Insatll nginx in it 
 
   - sudo apt update
   - ![image](https://user-images.githubusercontent.com/106643382/194303969-31a845ea-6fb2-46cc-8501-74ec71645bda.png)
   - sudo apt install nginx
   - sudo systemctl start nginx
   - sudo systemctl status nginx
   - ![image](https://user-images.githubusercontent.com/106643382/194305213-0e81676e-2354-48bb-b4e7-072e4d5a8395.png)
   - vim /var/www/html 
   - ![image](https://user-images.githubusercontent.com/106643382/194305528-8a7052a8-417a-4f04-9adb-de840316b7a1.png)
   - it will show on web server like this
   - ![image](https://user-images.githubusercontent.com/106643382/194306272-2f858b8f-8d76-440f-b1b2-047850c811cb.png)
   - Then attach elastic ip for server using [this](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)
   - ![image](https://user-images.githubusercontent.com/106643382/194306762-dd2361f6-d266-4062-a37a-8d67272a746f.png)
   - Then purchase a domain name for server from freenom (task1354.ml)
   - cd /etc/nginx/sites/task1354.ml
   - In this we have to give domain name
   - ![image](https://user-images.githubusercontent.com/106643382/194309542-d8254d64-6054-4627-bea1-3dc0617d0dfa.png)
   - nginx -t 
   - this will show every thing is ok
#### Install cetbox for SSL CERTIFICATION
   -  apt-get update
   -  sudo apt-get install certbot
   -  apt-get install python3-certbot-nginx
   -  
   - sudo certbot --nginx -d task1354.ml -d www.task1354.ml
   - This will issue certificate (in my case my domain name is task1354.ml)
   - ![image](https://user-images.githubusercontent.com/106643382/194316641-7c403bad-1eeb-4f86-8494-18df87a95637.png)
   - 
   ##### Configure automation script for SSL renewal.
   - 
   - sudo certbot renew --nginx
   - 
   - This will take you through the steps of renewal. LetsEncrypt will only allow renewal when the certificate is within 30 days of expiry. Once renewed the new certificate will be valid for 90 days from the date of renewal.

Renewing the certificate in this manner will not require you to stop and start Nginx and the Nginx config will be reloaded on a successful renewal so that visitors to the site are automatically served the new certificate. 

#### Automating The SSL Certificate Renewal For Nginx
```
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

0 */12 * * * root certbot -q renew --nginx

```
   - 
   - 
   - 

   - 


   - 
   - 
   


   - 


