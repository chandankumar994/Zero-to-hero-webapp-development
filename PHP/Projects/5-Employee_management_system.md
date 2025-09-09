## employee management system.

This will be a **complete mini Employee Management System** with:
✅ User authentication (Register, Login, Logout, Session)
✅ Dashboard with sidebar + topbar
✅ CRUD for employees (Add, View, Update, Delete)
✅ Bootstrap responsive design

---

# 📂 Project Structure

```
user_system/
│── db.php
│── login.php
│── register.php
│── dashboard.php
│── employees.php
│── add_employee.php
│── edit_employee.php
│── delete_employee.php
│── logout.php
```
---
# Database script (run in phpmyadmin)
```sql
-- Create Database
CREATE DATABASE IF NOT EXISTS user_system;
USE user_system;

-- Users table (for login/register system)
CREATE TABLE IF NOT EXISTS users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(100) NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Employees table (for CRUD operations)
CREATE TABLE IF NOT EXISTS employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    firstname VARCHAR(50) NOT NULL,
    lastname VARCHAR(50) NOT NULL,
    department VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL,
    country VARCHAR(50) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

```
---

# ⚙️ `db.php`

```php
<?php
$servername = "localhost";
$username = "root";   // change if needed
$password = "";       // change if needed
$dbname = "user_system";

$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
?>
```

---

# 🔐 `login.php`

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
  <title>Login - User System</title>
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

# 📝 `register.php`

```php
<?php
include 'db.php';

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $username = trim($_POST['username']);
    $email = trim($_POST['email']);
    $password = password_hash($_POST['password'], PASSWORD_DEFAULT);

    $check = "SELECT * FROM users WHERE username='$username'";
    $result = $conn->query($check);

    if ($result->num_rows > 0) {
        $error = "⚠ Username already exists!";
    } else {
        $sql = "INSERT INTO users (username, email, password) VALUES ('$username', '$email', '$password')";
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
  <title>Register - User System</title>
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
      <label class="form-label">Email</label>
      <input type="email" name="email" class="form-control" required>
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

# 📊 `dashboard.php`

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
  <title>Dashboard - User System</title>
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
  <h4>User System</h4>
  <a href="dashboard.php">🏠 Dashboard</a>
  <a href="employees.php">👥 Employees</a>
  <a href="logout.php">🚪 Logout</a>
</div>

<div class="content">
  <div class="topbar">
    <h5>Dashboard</h5>
    <span>Hi, <b><?= $username ?></b></span>
  </div>
  <div class="p-4">
    <h3>Welcome <?= $username ?> 🎉</h3>
    <p>This is your dashboard. Manage employees using the sidebar.</p>
  </div>
</div>

</body>
</html>
```

---

# 👥 `employees.php`

```php
<?php
include("db.php");
$result = mysqli_query($conn, "SELECT * FROM employees");
?>

<h3>Employees List</h3>
<a href="dashboard.php?page=add_employee" class="btn btn-primary mb-2">Add Employee</a>
<table class="table table-bordered">
    <tr>
        <th>ID</th>
        <th>First Name</th>
        <th>Last Name</th>
        <th>Department</th>
        <th>Email</th>
        <th>Country</th>
        <th>Actions</th>
    </tr>
    <?php while ($row = mysqli_fetch_assoc($result)) { ?>
    <tr>
        <td><?php echo $row['id']; ?></td>
        <td><?php echo $row['firstname']; ?></td>
        <td><?php echo $row['lastname']; ?></td>
        <td><?php echo $row['department']; ?></td>
        <td><?php echo $row['email']; ?></td>
        <td><?php echo $row['country']; ?></td>
        <td>
            <a href="dashboard.php?page=edit_employee&id=<?php echo $row['id']; ?>" class="btn btn-warning btn-sm">Edit</a>
            <a href="delete_employee.php?id=<?php echo $row['id']; ?>" class="btn btn-danger btn-sm"
               onclick="return confirm('Are you sure you want to delete this employee?');">Delete</a>
        </td>
    </tr>
    <?php } ?>
</table>
```

---

# ➕ `add_employee.php`

```php
<?php
include("db.php");

if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $firstname = $_POST['firstname'];
    $lastname = $_POST['lastname'];
    $department = $_POST['department'];
    $email = $_POST['email'];
    $country = $_POST['country'];

    $query = "INSERT INTO employees (firstname, lastname, department, email, country) 
              VALUES ('$firstname', '$lastname', '$department', '$email', '$country')";
    if (mysqli_query($conn, $query)) {
        header("Location: dashboard.php?page=employees");
        exit();
    } else {
        echo "<div class='alert alert-danger'>Error: " . mysqli_error($conn) . "</div>";
    }
}
?>

<h3>Add Employee</h3>
<form method="POST">
    <div class="mb-3">
        <label>First Name</label>
        <input type="text" name="firstname" class="form-control" required>
    </div>
    <div class="mb-3">
        <label>Last Name</label>
        <input type="text" name="lastname" class="form-control" required>
    </div>
    <div class="mb-3">
        <label>Department</label>
        <input type="text" name="department" class="form-control" required>
    </div>
    <div class="mb-3">
        <label>Email</label>
        <input type="email" name="email" class="form-control" required>
    </div>
    <div class="mb-3">
        <label>Country</label>
        <input type="text" name="country" class="form-control" required>
    </div>
    <button type="submit" class="btn btn-success">Add</button>
    <a href="dashboard.php?page=employees" class="btn btn-secondary">Cancel</a>
</form>

```

---

# ✏️ `edit_employee.php`

```php
<?php
include("db.php");

$id = $_GET['id'];
$result = mysqli_query($conn, "SELECT * FROM employees WHERE id=$id");
$employee = mysqli_fetch_assoc($result);

if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $firstname = $_POST['firstname'];
    $lastname = $_POST['lastname'];
    $department = $_POST['department'];
    $email = $_POST['email'];
    $country = $_POST['country'];

    $query = "UPDATE employees SET 
              firstname='$firstname', lastname='$lastname', department='$department', 
              email='$email', country='$country' WHERE id=$id";
    if (mysqli_query($conn, $query)) {
        header("Location: dashboard.php?page=employees");
        exit();
    } else {
        echo "<div class='alert alert-danger'>Error: " . mysqli_error($conn) . "</div>";
    }
}
?>

<h3>Edit Employee</h3>
<form method="POST">
    <div class="mb-3">
        <label>First Name</label>
        <input type="text" name="firstname" class="form-control" value="<?php echo $employee['firstname']; ?>" required>
    </div>
    <div class="mb-3">
        <label>Last Name</label>
        <input type="text" name="lastname" class="form-control" value="<?php echo $employee['lastname']; ?>" required>
    </div>
    <div class="mb-3">
        <label>Department</label>
        <input type="text" name="department" class="form-control" value="<?php echo $employee['department']; ?>" required>
    </div>
    <div class="mb-3">
        <label>Email</label>
        <input type="email" name="email" class="form-control" value="<?php echo $employee['email']; ?>" required>
    </div>
    <div class="mb-3">
        <label>Country</label>
        <input type="text" name="country" class="form-control" value="<?php echo $employee['country']; ?>" required>
    </div>
    <button type="submit" class="btn btn-primary">Update</button>
    <a href="dashboard.php?page=employees" class="btn btn-secondary">Cancel</a>
</form>

```

---

# ❌ `delete_employee.php`

```php
<?php
include 'db.php';
$id = $_GET['id'];
$conn->query("DELETE FROM employees WHERE id=$id");
header("Location: employees.php");
exit;
?>
```

---

# 🚪 `logout.php`

```php
<?php
session_start();
session_destroy();
header("Location: login.php");
exit;
?>
```

---
