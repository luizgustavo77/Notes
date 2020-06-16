# Composer centos
``` shell
yum install php72-php-bcmath.x86_64
cp /etc/opt/remi/php72/php.d/20-bcmath.ini /etc/php.d/
cp /opt/remi/php72/root/usr/lib64/php/modules/bcmath.so /usr/lib64/php/modules/
systemctl restart httpd
```