# Basic Nginx Deployment

#### Description:

- Create an EC2 server.
- Install Nginx in it.
- Create a sample index.html page and deploy it on that Nginx server.
- Create an elastic IP and attach it to the ec2 instance.
- Configure domain and apply SSL.
- Configure automation script for SSL renewal.

#### First step: Create an EC2 server

  - Firstly, log in to the AWS management console.
  - After login, navigate to the search bar, type EC2, and select EC2
  - Now, the EC2 dashboard will appear. Click Instances
  - Click the Launch instances button.
  - To launch an EC2 instance, a few details are required, i.e., instance name, OS image (AMI), instance type, etc.
  - Select a key pair to attach with the instance to log in with that key.
  - Click the Launch instance button
  - Take the public IP from the EC2 dashboard and use it to login inside the instance using ssh.
  - Finally, it will be logged in successfully if everything is configured correctly.
  
 #### Second Step:  Insatll nginx in it
 
   - First, update the list of packages using ```sudo apt update```
   - ![image](https://user-images.githubusercontent.com/106643382/194303969-31a845ea-6fb2-46cc-8501-74ec71645bda.png)
   - Now, install Nginx using ```sudo apt install nginx```
   - To start Nginx run this command ```sudo systemctl start nginx```
   - To check status of nginx ```sudo systemctl status nginx```
   - ![image](https://user-images.githubusercontent.com/106643382/194305213-0e81676e-2354-48bb-b4e7-072e4d5a8395.png)
   - To check whether Nginx is successfully installed or not, use ```sudo nginx -v```
   
   #### Third Step: Step Create a sample index.html page and deploy it on that Nginx server.
   
   - For this, navigate to document root ```vim /var/www/html``` and create an index.html page using vim or nano. 
   - ![image](https://user-images.githubusercontent.com/106643382/194305528-8a7052a8-417a-4f04-9adb-de840316b7a1.png)
   - For exit press Esc then press this : wq to exit.
   - it will show on web server like this
   - ![image](https://user-images.githubusercontent.com/106643382/194306272-2f858b8f-8d76-440f-b1b2-047850c811cb.png)
   - Then attach elastic ip for server using [this](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)
   - ![image](https://user-images.githubusercontent.com/106643382/194306762-dd2361f6-d266-4062-a37a-8d67272a746f.png)
   - Then purchase a domain name for server from freenom (task1354.ml)
   - ```cd /etc/nginx/sites-available/task1354.ml
   - In this we have to configure Domain name & Document root path 
   - ![image](https://user-images.githubusercontent.com/106643382/195326106-0906ae69-ced1-4895-8329-8584cfb963f6.png)
   - ![image](https://user-images.githubusercontent.com/106643382/195326248-2f5e5133-b319-401d-88d8-dbc44c62c68b.png)
   - ![image](https://user-images.githubusercontent.com/106643382/195326375-134d9092-adaa-48ce-828b-cc16e969b7c0.png)
   - ![image](https://user-images.githubusercontent.com/106643382/195326553-abb11cd1-11ed-400c-a20b-3c81eb7c1ae4.png)
   - In this we have to give domain name
   - ![image](https://user-images.githubusercontent.com/106643382/194309542-d8254d64-6054-4627-bea1-3dc0617d0dfa.png)
   - nginx -t 
   - this will show every thing is ok.
   
   #### Fourth step Insatall cetbox for SSL CERTIFICATION
   
   -` apt-get update
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
   
   - cat /etc/cron.d/certbot
   - ![image](https://user-images.githubusercontent.com/106643382/194525632-ff00a7ce-afbf-43d9-93f7-a8f7bcaad78c.png)
   - 
   - 
   - certbot renew --cert-name task1354.ml --force-renewal
   - 
   - ![image](https://user-images.githubusercontent.com/106643382/194526267-991ae8aa-61c0-4acd-aeaf-83ff923daa43.png)

   
   
   
      ######                                        THANK YOU 


