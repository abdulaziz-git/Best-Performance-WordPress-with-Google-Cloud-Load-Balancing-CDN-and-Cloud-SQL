# Best Performance WordPress with Google Cloud Load Balancing CDN and Cloud-SQL

## Command used in the video
### Installing WordOps
> reference: https://docs.wordops.net/getting-started/installation-guide/

```bash
sudo apt update
sudo apt install wget
wget -qO wo wops.cc && sudo bash wo
bash -l
echo -e "alias wo='sudo -E wo'" >> $HOME/.bashrc
source $HOME/.bashrc
```
------------------------------------------

### Creating WordPress Stack (NGINX, PHP, MySQL) with WordOps
> reference: https://docs.wordops.net/commands/site/#wordpress

```bash
wo site create YOURDOMAIN --wpfc --vhostonly
sudo wo stack remove --mysql
sudo wo stack install --mysqlclient
```
------------------------------------------

### Downloading and install WordPress

```bash
curl -LO https://wordpress.org/latest.tar.gz
tar xzvf latest.tar.gz
sudo cp -a wordpress/. /var/www/YOURDOMAIN/htdocs
rm latest.tar.gz
rm -rf wordpress
sudo chmod -R 755 /var/www/YOURDOMAIN/htdocs/
sudo chown -R www-data:www-data /var/www/YOURDOMAIN/htdocs/
cd /var/www/YOURDOMAIN/htdocs/
```
------------------------------------------

### Add this to wp-config.php file

```php
define('FS_METHOD', 'direct');

// This is for WordPress behind reverse proxy
define('FORCE_SSL_ADMIN', true);
if (strpos($_SERVER['HTTP_X_FORWARDED_PROTO'], 'https') !== false)
    $_SERVER['HTTPS']='on';
```
------------------------------------------

### Google Cloud Platform reference
- VPC Network: https://cloud.google.com/vpc/docs/create-modify-vpc-networks
- Compute Engine: https://cloud.google.com/compute/docs/instances/create-start-instance
- Cloud SQL for MySQL: https://cloud.google.com/sql/docs/mysql/create-instance
- Cloud Load Balancing: https://cloud.google.com/load-balancing/docs/https
- Cloud CDN: https://cloud.google.com/cdn/docs/setting-up-cdn-with-mig
- Cloud Storage: https://cloud.google.com/storage/docs

### Wordpress reference
- WordOps: https://wordops.net/
- Wordpress: https://wordpress.org/
- Nginx Helper: https://wordpress.org/plugins/nginx-helper/
- WP Offload Media Lite: https://wordpress.org/plugins/amazon-s3-and-cloudfront/

### Other reference
- Nginx: https://nginx.org/en/docs/
- PHP: https://www.php.net/docs.php
- MySQL Client: https://dev.mysql.com/doc/refman/8.0/en/mysql.html
