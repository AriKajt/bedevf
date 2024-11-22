# PHP Database Connection Guide

## MySQL Database Setup

### 1. Create Database via Command Line

#### Database Creation Steps:
```bash
# Login to MySQL
mysql -u root -p

# Input login credentials when prompted

# Create database
CREATE DATABASE example_db;

# Use the newly created database
USE example_db;

# Create users table
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

# Insert sample data
INSERT INTO users (username, email, password) 
VALUES 
('john_doe', 'john@example.com', 'password123'),
('jane_doe', 'jane@example.com', 'securepass');

# Verify data
SELECT * FROM users;
```

## PHP Database Connections

### 2. PDO Connection

#### a) Database Connection File (`db_connection.php`):
```php
<?php
$host = 'localhost';     // Database server
$db   = 'example_db';    // Your database name
$user = 'root';          // Your database username
$pass = '';              // Your database password
$charset = 'utf8mb4';

$dsn = "mysql:host=$host;dbname=$db;charset=$charset";
$options = [
    PDO::ATTR_ERRMODE            => PDO::ERRMODE_EXCEPTION,
    PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
    PDO::ATTR_EMULATE_PREPARES   => false,
];

try {
    $pdo = new PDO($dsn, $user, $pass, $options);
} catch (\PDOException $e) {
    throw new \PDOException($e->getMessage(), (int)$e->getCode());
}
```

#### b) User Controller (`user_controller.php`):
```php
<?php
// Include the PDO connection file
require 'db_connection.php';

// Fetch all users from the database
function getAllUsers($pdo) {
    $stmt = $pdo->query('SELECT * FROM users');
    return $stmt->fetchAll();
}

// Example usage of the getAllUsers function
$users = getAllUsers($pdo);
foreach ($users as $user) {
    echo "Username: " . $user['username'] . "<br>";
    echo "Email: " . $user['email'] . "<br>";
    echo "Created At: " . $user['created_at'] . "<br><br>";
}
```

### 3. MySQLi Connections

#### Object-Oriented Style:
```php
<?php
$servername = "localhost";
$username = "username";
$password = "password";

// Create connection
$conn = new mysqli($servername, $username, $password);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "Connected successfully";
?>
```

#### Procedural Style:
```php
<?php
$servername = "localhost";
$username = "username";
$password = "password";

// Create connection
$conn = mysqli_connect($servername, $username, $password);

// Check connection
if (!$conn) {
    die("Connection failed: " . mysqli_connect_error());
}
echo "Connected successfully";
?>
```
