PHP connection to database
    PDO:
        1. MySQL - Create database:
            a) mysql -u root -p
            b) input login data (myswl username and password)
            c) CREATE DATABASE example_db;
            d)USE example_db;
            e) CREATE TABLE users (
                id INT AUTO_INCREMENT PRIMARY KEY,
                username VARCHAR(50) NOT NULL,
                email VARCHAR(100) NOT NULL,
                password VARCHAR(255) NOT NULL,
                created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
                );
            f) INSERT INTO users (username, email, password) 
                VALUES 
                ('john_doe', 'john@example.com', 'password123'),
                ('jane_doe', 'jane@example.com', 'securepass');
            g) SELECT * FROM users;

        2) Create php pdo connection file, you can name it db_connection.php
            a) Insert data:
            <?php
            $host = 'localhost'; // Database server
            $db   = 'example_db'; // Your database name
            $user = 'root'; // Your database username
            $pass = ''; // Your database password - if there is no password set up leave blank
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

            b) Create a File Named user_controller.php
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

            c) Go to http://localhost:8000/user_controller.php to see the output.

        MySQLI - Object oriented:

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


        MySQLI - Procedural:

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

HTML form ready:

Login form