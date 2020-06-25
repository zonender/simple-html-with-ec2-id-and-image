# simple-html-with-ec2-id-and-image-merc

to install apache server on an instance via userdata:

user data:

```bash
#!/bin/bash
yum install httpd git -y
firewall-cmd --permanent --add-service=http
firewall-cmd --reload
systemctl start httpd
systemctl enable httpd
systemctl status httpd
rm -rf /var/www/html/merc
mkdir -p /var/www/html/merc
chown ec2-user:ec2-user /var/www/html/merc
chmod -R o+r /var/www/html/merc
git clone https://github.com/zonender/simple-html-with-ec2-id-and-image-merc.git /var/www/html/merc
ec2id=$(curl http://169.254.169.254/latest/meta-data/instance-id)
ec2ip=$(curl http://169.254.169.254/latest/meta-data/local-ipv4)
sed -i "s/ec2id/$ec2id/g" /var/www/html/merc/index.html
sed -i "s/ec2ip/$ec2ip/g" /var/www/html/merc/index.html
```

To run it from the command line directly:

```
sudo yum install httpd git -y
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --reload
sudo systemctl start httpd
sudo systemctl enable httpd
sudo systemctl status httpd
sudo rm -rf /var/www/html/merc
sudo mkdir -p /var/www/html/merc
sudo chown ec2-user:ec2-user /var/www/html/merc
sudo chmod -R o+r /var/www/html/merc
sudo git clone https://github.com/zonender/simple-html-with-ec2-id-and-image-merc.git /var/www/html/merc
ec2id=$(curl http://169.254.169.254/latest/meta-data/instance-id)
ec2ip=$(curl http://169.254.169.254/latest/meta-data/local-ipv4)
sudo sed -i "s/ec2id/$ec2id/g" /var/www/html/merc/index.html
sudo sed -i "s/ec2ip/$ec2ip/g" /var/www/html/merc/index.html
```
