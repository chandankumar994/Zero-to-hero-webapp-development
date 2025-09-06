# 🟢 PHP Tutorial (Form handling, File Handling, Error Handling, File Upload)

---

## 1. Form Handling (GET & POST)

👉 A **form** lets users send data to your PHP file.
Two ways to send data:

* **GET** → data shows in the URL.
* **POST** → data is hidden in the request body.

### Example (GET)

```html
<!-- file: get_form.html -->
<form method="get" action="get_process.php">
  Name: <input type="text" name="name"><br>
  Age: <input type="number" name="age"><br>
  <button type="submit">Submit</button>
</form>
```

```php
<!-- file: get_process.php -->
<?php
echo "Hello " . $_GET['name'] . ", you are " . $_GET['age'] . " years old.";
?>
```

👉 When you submit, check the URL — you’ll see `?name=John&age=20`.

---

### Example (POST)

```html
<!-- file: post_form.html -->
<form method="post" action="post_process.php">
  Username: <input type="text" name="username"><br>
  Password: <input type="password" name="password"><br>
  <button type="submit">Login</button>
</form>
```

```php
<!-- file: post_process.php -->
<?php
$username = $_POST['username'];
$password = $_POST['password'];

if ($username == "admin" && $password == "1234") {
    echo "Login successful!";
} else {
    echo "Invalid login!";
}
?>
```

---

✅ **Exercise**:

1. Make a form with fields: `name, email, message`.
2. Show them on the next page with `$_POST`.

---

## 2. File Handling (Read, Write, Append)

👉 Files let us **save and read data** (like a mini database).

### Write to a file

```php
<?php
$file = fopen("data.txt", "w"); // w = write (overwrites file)
fwrite($file, "Hello World!\n");
fclose($file);
echo "Data written!";
?>
```

### Append to a file

```php
<?php
$file = fopen("data.txt", "a"); // a = append (adds to file)
fwrite($file, "New line added!\n");
fclose($file);
echo "Data appended!";
?>
```

### Read a file

```php
<?php
$content = file_get_contents("data.txt");
echo nl2br($content); // nl2br = shows new lines in HTML
?>
```

---

✅ **Exercise**:

1. Write a PHP script that saves your name and age into `data.txt`.
2. Create another script to read and show the contents of `data.txt`.

---

## 3. Error Handling (try/catch, error reporting)

👉 Sometimes code breaks (file missing, divide by 0).
We can **catch errors** using `try...catch`.

### Example

```php
<?php
try {
    $num1 = 10;
    $num2 = 0;
    if ($num2 == 0) {
        throw new Exception("Cannot divide by zero!");
    }
    echo $num1 / $num2;
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
?>
```

---

✅ **Exercise**:

1. Write a script to divide two numbers. If the second is 0, show “Error: Cannot divide by zero”.

---

## 4. File Upload (images/documents)

👉 Upload lets users send files (like images).

### Upload form

```html
<!-- file: upload.html -->
<form method="post" action="upload.php" enctype="multipart/form-data">
  <input type="file" name="myfile"><br>
  <button type="submit">Upload</button>
</form>
```

### Upload handler

```php
<!-- file: upload.php -->
<?php
if (isset($_FILES['myfile'])) {
    $file = $_FILES['myfile'];

    // Move file to "uploads" folder
    move_uploaded_file($file['tmp_name'], "uploads/" . $file['name']);

    echo "File uploaded: " . $file['name'];
}
?>
```

👉 Create a folder called **uploads** in your project before testing.

---

✅ **Exercise**:

1. Upload an image file, then display it on the same page.
   (Hint: use `<img src='uploads/filename.png'>`)

---

# 🎯 Recap

* **Forms** → use `$_GET` or `$_POST` to get values.
* **Files** → read/write with `fopen`, `fwrite`, `file_get_contents`.
* **Errors** → catch problems with `try...catch`.
* **Uploads** → use a form with `enctype="multipart/form-data"` and `move_uploaded_file()`.

---

👉 This is the **beginner-friendly version**.
Would you like me to now **add small “mini projects”** (like *Guestbook*, *Image Gallery*, *Simple Login Form*) combining these 4 topics together? That way you can practice end-to-end.
