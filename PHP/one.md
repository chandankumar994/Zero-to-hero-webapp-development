### PHP tutorial
---


# PHP Training Guide

This guide is designed to take you from **beginner to advanced PHP development**, with hands-on examples for each topic.

---

## 🟢 Beginner Topics

### 1. What is PHP? Introduction & Installation
- **PHP (Hypertext Preprocessor)** is a server-side scripting language for web development.  
- To run PHP, you need a server (Apache, Nginx) and PHP installed.

**Example:**

```php
<?php
echo "Hello, World! Welcome to PHP.";
?>
```

---

### 2. Environment Setup (Local Server, XAMPP/Docker)

* **XAMPP**: Install XAMPP, start Apache, and place PHP files in `htdocs/`.
* **Docker**: Use PHP image.

**Docker Example:**

```dockerfile
FROM php:8.1-apache
COPY . /var/www/html/
```

---

### 3. Basic Syntax & Structure

```php
<?php
// Single-line comment
/*
 Multi-line comment
*/
echo "This is PHP Syntax!";
?>
```

---

### 4. Variables, Data Types, Constants, Operators

```php
<?php
$name = "John"; // String
$age = 25;      // Integer
$price = 99.99; // Float
$isAdmin = true; // Boolean

define("SITE_NAME", "MyWebsite");

echo $name . " is " . $age . " years old.";
?>
```

---

### 5. Control Structures (if, else, switch, loops)

```php
<?php
$marks = 75;

// if-else
if ($marks >= 50) {
    echo "Pass";
} else {
    echo "Fail";
}

// switch
$day = "Mon";
switch($day) {
    case "Mon": echo "Start of week"; break;
    default: echo "Other day"; break;
}

// loop
for ($i=1; $i<=5; $i++) {
    echo "Number: $i <br>";
}
?>
```

---

### 6. Arrays and Array Functions

```php
<?php
$fruits = ["Apple", "Banana", "Cherry"];
array_push($fruits, "Mango");

foreach($fruits as $fruit) {
    echo $fruit . "<br>";
}
?>
```

---

### 7. Functions (Built-in & User-defined)

```php
<?php
// Built-in
echo strlen("Hello PHP");

// User-defined
function greet($name) {
    return "Hello, " . $name;
}
echo greet("John");
?>
```

---

## 🟡 Intermediate Topics

### 1. Forms: GET & POST

**form.html**

```html
<form method="POST" action="process.php">
  Name: <input type="text" name="username">
  <input type="submit">
</form>
```

**process.php**

```php
<?php
$name = $_POST['username'];
echo "Hello, " . htmlspecialchars($name);
?>
```

---

### 2. File Handling

```php
<?php
// Write
file_put_contents("data.txt", "Hello File");

// Read
echo file_get_contents("data.txt");
?>
```

---

### 3. Sessions & Cookies

```php
<?php
// Session
session_start();
$_SESSION['user'] = "John";

// Cookie
setcookie("user", "John", time() + 3600);

echo $_SESSION['user'];
echo $_COOKIE['user'];
?>
```

---

### 4. Error Handling & Debugging

```php
<?php
try {
    if(!file_exists("data.txt")) {
        throw new Exception("File not found");
    }
} catch(Exception $e) {
    echo "Error: " . $e->getMessage();
}
?>
```

---

### 5. Dates & Times

```php
<?php
echo date("Y-m-d H:i:s");
$nextWeek = strtotime("+1 week");
echo date("Y-m-d", $nextWeek);
?>
```

---

### 6. Regular Expressions & String Manipulation

```php
<?php
$pattern = "/php/i";
$text = "I love PHP";
if (preg_match($pattern, $text)) {
    echo "Match found!";
}
?>
```

---

## 🟠 Database Integration

### 1. Introduction to MySQL/PostgreSQL

Install MySQL/PostgreSQL and create a database.

---

### 2. Connecting PHP to MySQL

```php
<?php
$conn = new mysqli("localhost", "root", "", "testdb");
if ($conn->connect_error) die("Connection failed");
echo "Connected!";
?>
```

---

### 3. CRUD Operations

```php
<?php
// Create
$conn->query("INSERT INTO users (name) VALUES ('John')");

// Read
$result = $conn->query("SELECT * FROM users");
while($row = $result->fetch_assoc()) {
    echo $row['name'];
}

// Update
$conn->query("UPDATE users SET name='Mike' WHERE id=1");

// Delete
$conn->query("DELETE FROM users WHERE id=1");
?>
```

---

### 4. Real-world Projects

* **Login System**: Verify user with database.
* **Blog**: Create posts and display.
* **To-do List**: Add/remove tasks.
* **Calculator**: Perform operations with PHP.

---

## 🔴 Advanced Concepts

### 1. OOP (Classes, Inheritance, Interfaces)

```php
<?php
class Animal {
    public $name;
    function __construct($name) { $this->name = $name; }
    function speak() { echo "$this->name makes a sound"; }
}

class Dog extends Animal {
    function speak() { echo "$this->name barks"; }
}

$dog = new Dog("Tommy");
$dog->speak();
?>
```

---

### 2. Security

```php
<?php
// Prevent SQL Injection
$stmt = $conn->prepare("SELECT * FROM users WHERE email=?");
$stmt->bind_param("s", $email);
$stmt->execute();

// Password Hashing
$hash = password_hash("mypassword", PASSWORD_DEFAULT);
if(password_verify("mypassword", $hash)) {
    echo "Valid login!";
}
?>
```

---

### 3. Working with APIs & AJAX

**api.php**

```php
<?php
$data = ["status" => "success", "message" => "Hello API"];
echo json_encode($data);
?>
```

**ajax.html**

```html
<script>
fetch("api.php")
.then(res => res.json())
.then(data => console.log(data));
</script>
```

---

### 4. Composer for Package Management

```bash
composer init
composer require monolog/monolog
```

---

### 5. Autoloading & Using Third-party Libraries

```php
<?php
require 'vendor/autoload.php';

use Monolog\Logger;
use Monolog\Handler\StreamHandler;

$log = new Logger('app');
$log->pushHandler(new StreamHandler('app.log', Logger::WARNING));
$log->warning('This is a warning!');
?>
```

---

# ✅ Conclusion

This documentation covers **PHP from basics to advanced**, with examples ready to run. Use this as a quick reference for training, practice, and real-world projects.

---

```

---

Would you like me to also **separate the examples into individual `.php` files** and provide a sample **folder structure for GitHub repo** (like `/beginner`, `/intermediate`, `/advanced`) so learners can run them directly?
```

