# Designmap Single Page Application

Latest features:

- app-layout
- app-routes
- styles inside tag
- polymer-cli


##### Prerequisites

    npm install -g polymer-cli

### Start

    npm start

### Build

    npm run build

### Test

    npm run test


Deploy

p 1. npm run build
ssh 2. ssh -i ~/.ssh/designmap-spa.pem ec2-user@ec2-52-57-8-122.eu-central-1.compute.amazonaws.com
ssh 3. sudo su & cd /var/www/html
ssh 4. rm -rf *
ssh 5. cd ../ & chmod 777 -R ./html
sftp 6. sftp -i ~/.ssh/designmap-spa.pem ec2-user@ec2-52-57-8-122.eu-central-1.compute.amazonaws.com
sftp 7. lcd /Users/kysonic/WebDevelopments/CDC/designmap-spa-v3/build/unbundled
sftp 8. cd /var/www/html
sftp 9. put -r .
ssh 10. service nginx restart
ssh 11. chmod 755 -R ./html

#Let's encrypt# Designmap Single Page Application

Latest features:

- app-layout
- app-routes
- styles inside tag
- polymer-cli


##### Prerequisites

  npm install -g polymer-cli

### Start

  npm start

### Build

  npm run build

### Test

  npm run test


Deploy

p 1. npm run build
ssh 2. ssh -i ~/.ssh/designmap-spa.pem ec2-user@ec2-52-57-8-122.eu-central-1.compute.amazonaws.com
ssh 3. cd /var/www/html
ssh 4. rm -rf *
ssh 5. cd ../ && chmod 777 -R ./html
sftp 6. sftp -i ~/.ssh/designmap-spa.pem ec2-user@ec2-52-57-8-122.eu-central-1.compute.amazonaws.com
sftp 7. lcd /Users/kysonic/WebDevelopments/CDC/designmap-spa-v3/build/unbundled
sftp 8. cd /var/www/html
sftp 9. put -r .
ssh 10. service nginx restart
ssh 11. chmod 755 -R ./html

#Let's encrypt

https://coderwall.com/p/e7gzbq/https-with-certbot-for-nginx-on-amazon-linux

certbot is already installed:

  /usr/local/bin - certbot-auto

To make renew of certificate:

  ./certbot-auto renew --dry-run --debug

To make new one if it will be needed:

 ./certbot-auto certonly --standalone -d app.designmap.ru --debug

The folder of letsencrypt:

 /etc/letsencrypt/...

#Problems

zope.interface error:

unset PYTHON_INSTALL_LAYOUT; /root/certbot-auto --debug renew


https://coderwall.com/p/e7gzbq/https-with-certbot-for-nginx-on-amazon-linux

certbot is already installed:

    /usr/local/bin - certbot-auto

To make renew of certificate:

    ./certbot-auto renew --dry-run --debug

To make new one if it will be needed:

   ./certbot-auto certonly --standalone -d app.designmap.ru --debug

The folder of letsencrypt:

   /etc/letsencrypt/...

#Problems

zope.interface error:

unset PYTHON_INSTALL_LAYOUT; /root/certbot-auto --debug renew
