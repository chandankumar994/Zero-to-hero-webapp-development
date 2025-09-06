# 📝 Mini Project: Simple Guestbook

👉 What it does:

* Users can **submit their name and a message** through a form.
* Messages are **saved in a file (CSV)**.
* All messages are displayed on the page.
* If something goes wrong (like file not found), we **handle errors**.
* Optionally: users can **upload an image** with their message.

---

## 📂 Project Structure

```
guestbook/
│
├── index.php        (form + show messages)
├── save.php         (process form & save data)
├── uploads/         (folder for uploaded images)
├── data.csv         (stores name, message, image)
```

---

## 1. Form & Display (index.php)

```php
<!doctype html>
<html>
<head>
  <title>Simple Guestbook</title>
</head>
<body>
  <h1>Guestbook</h1>

  <!-- Form -->
  <form action="save.php" method="post" enctype="multipart/form-data">
    Name: <input type="text" name="name" required><br><br>
    Message:<br>
    <textarea name="message" required></textarea><br><br>
    Upload Image (optional): <input type="file" name="image"><br><br>
    <button type="submit">Post</button>
  </form>
  <hr>

  <h2>Messages:</h2>
  <?php
  $file = "data.csv";
  if (file_exists($file)) {
      if (($handle = fopen($file, "r")) !== false) {
          while (($row = fgetcsv($handle)) !== false) {
              $name = htmlspecialchars($row[0]);
              $message = htmlspecialchars($row[1]);
              $image = $row[2];

              echo "<p><strong>$name</strong>: $message</p>";
              if ($image != "") {
                  echo "<img src='uploads/$image' width='100'><br>";
              }
              echo "<hr>";
          }
          fclose($handle);
      }
  } else {
      echo "<p>No messages yet.</p>";
  }
  ?>
</body>
</html>
```

---

## 2. Save Data (save.php)

```php
<?php
try {
    $name = $_POST['name'] ?? '';
    $message = $_POST['message'] ?? '';
    $imageName = "";

    // Handle file upload (if any)
    if (!empty($_FILES['image']['name'])) {
        $uploadDir = "uploads/";
        if (!is_dir($uploadDir)) {
            mkdir($uploadDir);
        }
        $imageName = basename($_FILES['image']['name']);
        move_uploaded_file($_FILES['image']['tmp_name'], $uploadDir . $imageName);
    }

    // Save to CSV file
    $file = fopen("data.csv", "a");
    if (!$file) {
        throw new Exception("Cannot open file!");
    }
    fputcsv($file, [$name, $message, $imageName]);
    fclose($file);

    // Redirect back
    header("Location: index.php");
    exit;
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
?>
```

---

## 🎯 How it uses all 4 topics

1. **Form Handling** → `$_POST` for name & message.
2. **File Handling** → store messages in `data.csv`, read with `fgetcsv()`.
3. **Error Handling** → `try...catch` when saving.
4. **File Upload** → users can upload images (saved in `uploads/`).

---

## ✅ Exercise Ideas

1. Add a **date/time** field to each message.
2. Show newest messages **on top**.
3. Limit image upload to only `.jpg` and `.png`.
4. Create a “Delete all messages” button (clear `data.csv`).
