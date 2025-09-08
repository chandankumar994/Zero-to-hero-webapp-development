# 🐘 PHP + MySQL CRUD Tutorial for Beginners

CRUD means:

* **C**reate → Insert new record
* **R**ead → Select & display records
* **U**pdate → Edit records
* **D**elete → Remove records

We’ll make a simple **Employee Management System** with fields:
`ID, Firstname, Lastname, Department, Email, Country`

---

## 1️⃣ Create Database and Table

First, open **phpMyAdmin** or MySQL terminal and run:

```sql
CREATE DATABASE company_db;

USE company_db;

CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    firstname VARCHAR(50),
    lastname VARCHAR(50),
    department VARCHAR(100),
    email VARCHAR(100),
    country VARCHAR(50)
);
```

---

## 2️⃣ Connect PHP with MySQL (db.php)

Create a file `db.php` to handle the database connection:

```php
<?php
$host = "localhost";   // usually localhost
$user = "root";        // your MySQL username
$pass = "";            // your MySQL password
$db   = "company_db";  // database name

$conn = new mysqli($host, $user, $pass, $db);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
?>
```

---

## 3️⃣ Show Records (index.php)

```php
<?php
include 'db.php';

// Fetch all employees
$sql = "SELECT * FROM employees";
$result = $conn->query($sql);
?>
<!doctype html>
<html>
<head>
    <title>Employee Records</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
</head>
<body class="container mt-5">

<h2>Employee List</h2>
<a href="create.php" class="btn btn-success mb-3">+ Add New Employee</a>

<table class="table table-bordered table-striped">
    <tr>
        <th>ID</th><th>Firstname</th><th>Lastname</th>
        <th>Department</th><th>Email</th><th>Country</th><th>Action</th>
    </tr>
    <?php while($row = $result->fetch_assoc()) { ?>
    <tr>
        <td><?= $row['id'] ?></td>
        <td><?= $row['firstname'] ?></td>
        <td><?= $row['lastname'] ?></td>
        <td><?= $row['department'] ?></td>
        <td><?= $row['email'] ?></td>
        <td><?= $row['country'] ?></td>
        <td>
            <a href="details.php?id=<?= $row['id'] ?>" class="btn btn-info btn-sm">Details</a>
            <a href="edit.php?id=<?= $row['id'] ?>" class="btn btn-warning btn-sm">Edit</a>
            <a href="delete.php?id=<?= $row['id'] ?>" class="btn btn-danger btn-sm" onclick="return confirm('Are you sure?')">Delete</a>
        </td>
    </tr>
    <?php } ?>
</table>

</body>
</html>
```

---

## 4️⃣ Insert New Record (create.php)

```php
<?php
include 'db.php';

if ($_SERVER['REQUEST_METHOD'] == "POST") {
    $firstname = $_POST['firstname'];
    $lastname  = $_POST['lastname'];
    $dept      = $_POST['department'];
    $email     = $_POST['email'];
    $country   = $_POST['country'];

    $sql = "INSERT INTO employees (firstname, lastname, department, email, country)
            VALUES ('$firstname', '$lastname', '$dept', '$email', '$country')";

    if ($conn->query($sql)) {
        header("Location: index.php");
    } else {
        echo "Error: " . $conn->error;
    }
}
?>

<!doctype html>
<html>
<head>
    <title>Add Employee</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
</head>
<body class="container mt-5">
<h2>Add New Employee</h2>
<form method="post">
    <input class="form-control mb-2" type="text" name="firstname" placeholder="First Name" required>
    <input class="form-control mb-2" type="text" name="lastname" placeholder="Last Name" required>
    <input class="form-control mb-2" type="text" name="department" placeholder="Department" required>
    <input class="form-control mb-2" type="email" name="email" placeholder="Email" required>
    <input class="form-control mb-2" type="text" name="country" placeholder="Country" required>
    <button class="btn btn-success" type="submit">Save</button>
    <a href="index.php" class="btn btn-secondary">Cancel</a>
</form>
</body>
</html>
```

---

## 5️⃣ Edit Record (edit.php)

```php
<?php
include 'db.php';
$id = $_GET['id'];

// Get current record
$result = $conn->query("SELECT * FROM employees WHERE id=$id");
$row = $result->fetch_assoc();

if ($_SERVER['REQUEST_METHOD'] == "POST") {
    $firstname = $_POST['firstname'];
    $lastname  = $_POST['lastname'];
    $dept      = $_POST['department'];
    $email     = $_POST['email'];
    $country   = $_POST['country'];

    $sql = "UPDATE employees SET 
            firstname='$firstname', lastname='$lastname',
            department='$dept', email='$email', country='$country'
            WHERE id=$id";

    if ($conn->query($sql)) {
        header("Location: index.php");
    } else {
        echo "Error: " . $conn->error;
    }
}
?>

<!doctype html>
<html>
<head>
    <title>Edit Employee</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
</head>
<body class="container mt-5">
<h2>Edit Employee</h2>
<form method="post">
    <input class="form-control mb-2" type="text" name="firstname" value="<?= $row['firstname'] ?>" required>
    <input class="form-control mb-2" type="text" name="lastname" value="<?= $row['lastname'] ?>" required>
    <input class="form-control mb-2" type="text" name="department" value="<?= $row['department'] ?>" required>
    <input class="form-control mb-2" type="email" name="email" value="<?= $row['email'] ?>" required>
    <input class="form-control mb-2" type="text" name="country" value="<?= $row['country'] ?>" required>
    <button class="btn btn-primary" type="submit">Update</button>
    <a href="index.php" class="btn btn-secondary">Cancel</a>
</form>
</body>
</html>
```

---

## 6️⃣ Delete Record (delete.php)

```php
<?php
include 'db.php';
$id = $_GET['id'];

$conn->query("DELETE FROM employees WHERE id=$id");

header("Location: index.php");
?>
```

---

## 7️⃣ Show Details (details.php)

```php
<?php
include 'db.php';
$id = $_GET['id'];

$result = $conn->query("SELECT * FROM employees WHERE id=$id");
$row = $result->fetch_assoc();
?>
<!doctype html>
<html>
<head>
    <title>Employee Details</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
</head>
<body class="container mt-5">
<h2>Employee Details</h2>
<ul class="list-group">
    <li class="list-group-item"><strong>ID:</strong> <?= $row['id'] ?></li>
    <li class="list-group-item"><strong>Firstname:</strong> <?= $row['firstname'] ?></li>
    <li class="list-group-item"><strong>Lastname:</strong> <?= $row['lastname'] ?></li>
    <li class="list-group-item"><strong>Department:</strong> <?= $row['department'] ?></li>
    <li class="list-group-item"><strong>Email:</strong> <?= $row['email'] ?></li>
    <li class="list-group-item"><strong>Country:</strong> <?= $row['country'] ?></li>
</ul>
<br>
<a href="index.php" class="btn btn-secondary">Back</a>
</body>
</html>
```

---

# 🎯 Learning Points

* **Database Connection** → `db.php`
* **Select (Read)** → `index.php`
* **Insert (Create)** → `create.php`
* **Update (Edit)** → `edit.php`
* **Delete** → `delete.php`
* **Details View** → `details.php`

---

👉 This gives you a complete **CRUD system in PHP + MySQL** with Bootstrap styling, like the table in your image.
