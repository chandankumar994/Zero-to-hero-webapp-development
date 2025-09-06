# 🔑 Mini Project 3: Simple Login System

👉 What it does:

* User can **register** with a username & password.
* Data is saved in a file (`users.csv`).
* User can **log in** with the same details.
* If login succeeds → show a welcome page.
* If login fails → show error.
* User can **log out**.

---

## 📂 Project Structure

```
login-system/
│
├── register.php      (registration form + save user)
├── login.php         (login form + verify user)
├── welcome.php       (protected page after login)
├── logout.php        (end session)
├── users.csv         (stores username + password)
```

---

## 1. Registration Page (register.php)

```php
<?php
if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $username = $_POST['username'] ?? '';
    $password = $_POST['password'] ?? '';

    if ($username == "" || $password == "") {
        echo "All fields are required!";
    } else {
        // Save to CSV (with hashed password for safety)
        $file = fopen("users.csv", "a");
        fputcsv($file, [$username, password_hash($password, PASSWORD_DEFAULT)]);
        fclose($file);

        echo "Registration successful! <a href='login.php'>Login here</a>";
        exit;
    }
}
?>
<!doctype html>
<html>
<head><title>Register</title></head>
<body>
  <h1>Register</h1>
  <form method="post">
    Username: <input type="text" name="username" required><br><br>
    Password: <input type="password" name="password" required><br><br>
    <button type="submit">Register</button>
  </form>
</body>
</html>
```

---

## 2. Login Page (login.php)

```php
<?php
session_start();

if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $username = $_POST['username'] ?? '';
    $password = $_POST['password'] ?? '';

    if (($file = fopen("users.csv", "r")) !== false) {
        $found = false;
        while (($row = fgetcsv($file)) !== false) {
            if ($row[0] === $username && password_verify($password, $row[1])) {
                $found = true;
                break;
            }
        }
        fclose($file);

        if ($found) {
            $_SESSION['user'] = $username;
            header("Location: welcome.php");
            exit;
        } else {
            echo "Invalid username or password!";
        }
    } else {
        echo "No users registered yet!";
    }
}
?>
<!doctype html>
<html>
<head><title>Login</title></head>
<body>
  <h1>Login</h1>
  <form method="post">
    Username: <input type="text" name="username" required><br><br>
    Password: <input type="password" name="password" required><br><br>
    <button type="submit">Login</button>
  </form>
</body>
</html>
```

---

## 3. Welcome Page (welcome.php)

```php
<?php
session_start();
if (!isset($_SESSION['user'])) {
    header("Location: login.php");
    exit;
}
?>
<!doctype html>
<html>
<head><title>Welcome</title></head>
<body>
  <h1>Welcome, <?php echo htmlspecialchars($_SESSION['user']); ?>!</h1>
  <p>You are now logged in.</p>
  <a href="logout.php">Logout</a>
</body>
</html>
```

---

## 4. Logout Page (logout.php)

```php
<?php
session_start();
session_destroy();
header("Location: login.php");
exit;
?>
```

---

# 🎯 How this uses PHP basics

1. **Form Handling** → register & login forms use `$_POST`.
2. **File Handling** → users saved in `users.csv`.
3. **Error Handling** → check empty fields, wrong login.
4. **Session Handling** → keep track of logged-in users.

---

## ✅ Exercise Ideas

1. Add an **email field** to registration and show it on welcome page.
2. Prevent duplicate usernames (check before saving in `users.csv`).
3. Add a **“Change Password”** page.
4. Limit login attempts (after 3 wrong tries, block for a while).

---

Would you like me to **bundle these 3 projects into a single "mini portal"** (like a website with navigation links)? That way, all features are together in one project.
