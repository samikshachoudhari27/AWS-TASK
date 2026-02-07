
1. Application 
 Simple frontend + backend app 
 Use one database (MySQL / MongoDB / Influx DB) 
 App must connect to the database successfully 

This project demonstrates the deployment of a complete Linux, Apache, MySQL/MariaDB, PHP stack on an AWS EC2 instance (Free Tier) and the development of a simple PHP web application that connects to a MySQL database.

The application allows users to submit their name and email through a form and stores the data in a MariaDB database.

---

# Architecture

```
User Browser
      |
      |  (HTTP - Port 80)
      v
EC2 Instance (Amazon Linux)
   ├── Apache (Web Server)
   ├── PHP
   └── MariaDB (Database)
```

---

# Technologies Used

- AWS EC2 (t2.micro – Free Tier)
- Amazon Linux 2023
- Apache (httpd)
- MariaDB 10.5
- PHP
- HTML
- Linux CLI

---

# EC2 Configuration

| Setting            | Value |
|-------------------|-------|
| AMI               | Amazon Linux |
| Instance Type     | t2.micro |
| Public IP         | Enabled |
| Security Group    | SSH, HTTP, HTTPS |

# Security Group Rules

| Type  | Port | Source |
|-------|------|--------|
| SSH   | 22   | My IP |
| HTTP  | 80   | 0.0.0.0/0 |
| HTTPS | 443  | 0.0.0.0/0 |

---

# Installation Steps

# 1 Update System

```bash
sudo dnf update -y
```

---

# 2 Install Apache

```bash
sudo dnf install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```

Verify:
```
http://<EC2-Public-IP>
```

---

# 3 Install MariaDB

```bash
sudo dnf install mariadb105-server -y
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

Secure installation:

```bash
sudo mysql_secure_installation
```

---

# 4 Install PHP

```bash
sudo dnf install php php-mysqlnd -y
sudo systemctl restart httpd
```

Verify:

```bash
php -v
```

---

# Database Setup

Login to MySQL:

```bash
mysql -u root -p
```

Run:

```sql
CREATE DATABASE lampdb;

USE lampdb;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100)
);

CREATE USER 'lampuser'@'localhost' IDENTIFIED BY 'password123';
GRANT ALL PRIVILEGES ON lampdb.* TO 'lampuser'@'localhost';
FLUSH PRIVILEGES;
```

---

# Application Structure

```
/var/www/html
│
├── index.php        # PHP Info test page
├── config.php       # Database connection file
├── insert.php       # Handles form submission
└── form.html        # User input form
```

---

# Application Files

# config.php

Handles database connection.

```php
<?php
$servername = "localhost";
$username = "lampuser";
$password = "password123";
$database = "lampdb";

$conn = new mysqli($servername, $username, $password, $database);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
?>
```

---

# insert.php

Inserts user data into database.

```php
<?php
include 'config.php';

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $name = $_POST['name'];
    $email = $_POST['email'];

    $sql = "INSERT INTO users (name, email) VALUES ('$name', '$email')";

    if ($conn->query($sql) === TRUE) {
        echo "Record inserted successfully";
    } else {
        echo "Error: " . $conn->error;
    }
}

$conn->close();
?>
```

---

# How to Run

1. Open in browser:
   ```
   http://<EC2-Public-IP>/form.html
   ```

2. Enter name and email.
3. Submit the form.
4. Verify data inside MySQL:

```sql
SELECT * FROM users;
```

---

# Sample Output

```
Record inserted successfully
```

---

# Key Learning Outcomes

- EC2 provisioning and configuration
- Linux server management
- Apache web server setup
- MariaDB database configuration
- PHP and MySQL integration
- Web application deployment on AWS
- Security group configuration

User → Load Balancer → EC2 (Apache + PHP) → Maria db


