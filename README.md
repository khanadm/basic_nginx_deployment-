# Basic Nginx Deployment

#### Description:

- Create an EC2 server.
- Install Nginx in it.
- Create a sample index.html page and deploy it on that Nginx server.
- Create an elastic IP and attach it to the ec2 instance.
- Configure domain and apply SSL.
- Configure automation script for SSL renewal.

---

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
  
  ---
  
 #### Second Step:  Insatll nginx in it
 
   - First, update the list of packages using ```sudo apt update```
     
   - Now, install Nginx using ```sudo apt install nginx```
    
   - To start Nginx run this command ```sudo systemctl start nginx```
    
   - To check status of nginx ```sudo systemctl status nginx```
   
     ![image](https://user-images.githubusercontent.com/106643382/194305213-0e81676e-2354-48bb-b4e7-072e4d5a8395.png)
     
   - To enable nginx Run this command ```sudo systemctl enable nginx``` 
     
   - To check whether Nginx is successfully installed or not, use ```sudo nginx -v```
   
   
   ---


   
   #### Third Step: Step Create a sample index.html page and deploy it on that Nginx server.
   
   
   
   - For this, navigate to document root ```cd /var/www/html``` and create an index.html page using vim or nano.
  
   - For exit press Esc then press this : wq to exit.
   
   - We have hit IP It will show on web server like this.
  
     ![image](https://user-images.githubusercontent.com/106643382/196166855-db2adc87-44fe-48c7-b4e4-74995cf12de7.png)

   - Then attach elastic ip for server using [this](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)
  
     ![image](https://user-images.githubusercontent.com/106643382/194306762-dd2361f6-d266-4062-a37a-8d67272a746f.png)
     
   - Then purchase a domain name for server from freenom (task1354.ml)
   
   ![image](https://user-images.githubusercontent.com/106643382/196352696-7b03715f-1627-40f9-8d99-07ed702fe46f.png)
   
   - This is the configuration file of nginx ```vim /etc/nginx/sites-available/task1354.ml```
   
   - In this we have to configure Server name & Document root path 
   
     ![image](https://user-images.githubusercontent.com/106643382/195326106-0906ae69-ced1-4895-8329-8584cfb963f6.png)
     
     ![image](https://user-images.githubusercontent.com/106643382/195326248-2f5e5133-b319-401d-88d8-dbc44c62c68b.png)
     
     ![image](https://user-images.githubusercontent.com/106643382/195326375-134d9092-adaa-48ce-828b-cc16e969b7c0.png)
     
     ![image](https://user-images.githubusercontent.com/106643382/195326553-abb11cd1-11ed-400c-a20b-3c81eb7c1ae4.png)
     
   - In this we have to give domain name
   
     ![image](https://user-images.githubusercontent.com/106643382/194309542-d8254d64-6054-4627-bea1-3dc0617d0dfa.png)
     
   - To check that there are no syntax errors in any of your Nginx files, use ```sudo nginx -t```
   
   - This will show every thing is ok.


---
   
   #### Fourth step : Insatall cetbox for SSL CERTIFICATION
   
   - ```sudo apt-get update```
   
   - To obtain an SSL certificate, we must install certbot software and the Nginx plugin. ```apt-get certbot install python3-certbot-nginx```
   
   - To obtain a certificate for a domain. ```sudo certbot --nginx -d task1354.ml -d www.task1354.ml```
   
   - This will issue certificate (in my case my domain name is task1354.ml)
  
   ![image](https://user-images.githubusercontent.com/106643382/194316641-7c403bad-1eeb-4f86-8494-18df87a95637.png)
   
   
  ---
   
   #### Fifth Step : Configure automation script for SSL renewal .
 
  
    First Install certbot 
    
    ```sudo apt-get insatll certbot python3-certbot-nginx certbot``` 
   
   This will open the corn job file 
   
   ``` corntab -e```
   
   In bottom  we have to configure Automation parameter According to need along with Domain name.
   
   ```* * * * * certbot renew --nginix -d task1354.ml -d www.task1354.ml``` 


   
   
   ---
      ######                                        THANK YOU 


