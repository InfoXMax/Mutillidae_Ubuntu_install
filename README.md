# Mutillidae Installation Guide on Ubuntu 24.04

This guide provides step-by-step instructions to install Mutillidae on an Ubuntu 24.04 server.

## Prerequisites

Ensure you have the following installed:
- PHP 8.*
- Apache2
- MySQL Server

## Installation Steps

1. Install required PHP modules:
    ```bash
    sudo apt install php8.*-curl php8.*-mbstring php8.*-xml
    ```

2. Clone the Mutillidae repository:
    ```bash
    sudo git clone https://github.com/webpwnized/mutillidae.git
    ```

3. Install and configure Apache2:
    ```bash
    sudo apt install apache2
    sudo a2enmod rewrite
    sudo systemctl restart apache2
    ```

4. Edit Apache configuration file:
    ```bash
    sudo nano /etc/apache2/apache2.conf
    ```
    Ensure the following line is present:
    ```
    <Directory /var/www/html>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
    ```
    Restart Apache2:
    ```bash
    sudo systemctl restart apache2
    ```

5. Install PHP and MySQL support for Apache:
    ```bash
    sudo apt install php libapache2-mod-php
    sudo apt install mysql-server php-mysql
    sudo systemctl restart apache2
    ```

6. Configure MySQL:
    ```bash
    sudo mysql -u root
    ```
    Execute the following commands in the MySQL shell:
    ```sql
    ALTER USER 'root'@'localhost' IDENTIFIED BY 'mutillidae';
    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'mutillidae';
    FLUSH PRIVILEGES;
    EXIT;
    ```
    Restart Apache2 and MySQL:
    ```bash
    sudo systemctl restart apache2
    sudo systemctl restart mysql
    ```

7. Allow MySQL through the firewall:
    ```bash
    sudo ufw allow 3306
    sudo ufw reload
    ```

8. Set up the Mutillidae database:
    Open your browser and navigate to:
    ```
    http://your-server-ip/mutillidae/set-up-database.php
    ```

## Final Steps

After following these steps, your Mutillidae installation should be up and running on your Ubuntu 24.04 server. Access the application via your web browser at:
http://your-server-ip/mutillidae/


## Troubleshooting

- Ensure all services are running:
    ```bash
    sudo systemctl status apache2
    sudo systemctl status mysql
    ```
- Check firewall settings if you have connectivity issues.

## License

This project is licensed under the MIT License.
