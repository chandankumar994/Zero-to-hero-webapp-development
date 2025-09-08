# Employee Management system.
It will include:

✅ Database connection
✅ Login page (with error messages, session start)
✅ Register page (with password hashing)
✅ Dashboard page (with sidebar + top navbar + “Hi Username”)
✅ Logout

---

# 📂 Project Structure

```
employee_app/
│── db.php
│── login.php
│── register.php
│── dashboard.php
│── logout.php
```

---

# 🗄 1. Database Setup

Run this SQL in **phpMyAdmin / MySQL**:

```sql
CREATE DATABASE employee_app;

USE employee_app;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(100) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

# ⚙️ 2. `db.php`

```php
<?php
$servername = "localhost";
$username = "root";   // change if needed
$password = "";       // change if needed
$dbname = "employee_app";

$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
?>
```

---

# 🔐 3. `login.php`

```php
<?php
session_start();
include 'db.php';

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $username = trim($_POST['username']);
    $password = trim($_POST['password']);

    $sql = "SELECT * FROM users WHERE username='$username'";
    $result = $conn->query($sql);

    if ($result->num_rows == 1) {
        $row = $result->fetch_assoc();
        if (password_verify($password, $row['password'])) {
            $_SESSION['username'] = $row['username'];
            header("Location: dashboard.php");
            exit;
        } else {
            $error = "❌ Wrong password!";
        }
    } else {
        $error = "❌ User not found!";
    }
}
?>
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Login - Employee App</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
  <style>
    body {background: #343a40; display: flex; align-items: center; justify-content: center; height: 100vh;}
    .card {width: 360px; padding: 20px; border-radius: 12px; box-shadow: 0 4px 10px rgba(0,0,0,.2);}
  </style>
</head>
<body>
<div class="card">
  <h3 class="text-center mb-3">🔐 Login</h3>
  <?php if (!empty($error)): ?><div class="alert alert-danger"><?= $error ?></div><?php endif; ?>
  <form method="POST">
    <div class="mb-3">
      <label class="form-label">Username</label>
      <input type="text" name="username" class="form-control" required>
    </div>
    <div class="mb-3">
      <label class="form-label">Password</label>
      <input type="password" name="password" class="form-control" required>
    </div>
    <button type="submit" class="btn btn-dark w-100">Login</button>
  </form>
  <p class="mt-3 text-center">New here? <a href="register.php">Register</a></p>
</div>
</body>
</html>
```

---

# 📝 4. `register.php`

```php
<?php
include 'db.php';

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $username = trim($_POST['username']);
    $password = password_hash($_POST['password'], PASSWORD_DEFAULT);

    $check = "SELECT * FROM users WHERE username='$username'";
    $result = $conn->query($check);

    if ($result->num_rows > 0) {
        $error = "⚠ Username already exists!";
    } else {
        $sql = "INSERT INTO users (username, password) VALUES ('$username', '$password')";
        if ($conn->query($sql) === TRUE) {
            header("Location: login.php?registered=1");
            exit;
        } else {
            $error = "❌ Error: " . $conn->error;
        }
    }
}
?>
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Register - Employee App</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
  <style>
    body {background: #495057; display: flex; align-items: center; justify-content: center; height: 100vh;}
    .card {width: 380px; padding: 20px; border-radius: 12px; box-shadow: 0 4px 10px rgba(0,0,0,.2);}
  </style>
</head>
<body>
<div class="card">
  <h3 class="text-center mb-3">📝 Register</h3>
  <?php if (!empty($error)): ?><div class="alert alert-danger"><?= $error ?></div><?php endif; ?>
  <form method="POST">
    <div class="mb-3">
      <label class="form-label">Username</label>
      <input type="text" name="username" class="form-control" required>
    </div>
    <div class="mb-3">
      <label class="form-label">Password</label>
      <input type="password" name="password" class="form-control" required>
    </div>
    <button type="submit" class="btn btn-success w-100">Register</button>
  </form>
  <p class="mt-3 text-center">Already have an account? <a href="login.php">Login</a></p>
</div>
</body>
</html>
```

---

# 📊 5. `dashboard.php`

```php
<?php
session_start();
if (!isset($_SESSION['username'])) {
    header("Location: login.php");
    exit;
}
$username = $_SESSION['username'];
?>
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Dashboard - Employee App</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
  <style>
    body {display: flex; min-height: 100vh;}
    .sidebar {width: 220px; background: #212529; color: white; padding: 20px;}
    .sidebar a {color: #ccc; display: block; padding: 10px; text-decoration: none;}
    .sidebar a:hover {background: #343a40; color: #fff;}
    .content {flex-grow: 1;}
    .topbar {background: #f8f9fa; padding: 10px 20px; display: flex; justify-content: space-between; align-items: center;}
  </style>
</head>
<body>

<div class="sidebar">
  <h4>Employee App</h4>
  <a href="dashboard.php">🏠 Dashboard</a>
  <a href="#">👤 Profile</a>
  <a href="#">⚙ Settings</a>
  <a href="logout.php">🚪 Logout</a>
</div>

<div class="content">
  <div class="topbar">
    <h5>Dashboard</h5>
    <span>Hi, <b><?= $username ?></b></span>
  </div>
  <div class="p-4">
    <h3>Welcome <?= $username ?> 🎉</h3>
    <p>This is your dashboard. You can add features like employee management here.</p>
  </div>
</div>

</body>
</html>
```

---

# 🚪 6. `logout.php`

```php
<?php
session_start();
session_destroy();
header("Location: login.php");
exit;
?>
```

---

# ✅ Features in This Version

* Bootstrap-based, **modern responsive design**
* **Login/Register** with password hashing
* **Session management**
* **Dashboard with sidebar + topbar**
* **Logout functionality**
