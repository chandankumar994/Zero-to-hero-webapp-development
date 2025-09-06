# 🖼️ Mini Project 2: Simple Image Gallery

👉 What it does:

* Users can **upload images**.
* Images are saved in an `uploads/` folder.
* All uploaded images are displayed in a **gallery**.
* Errors (wrong file type, too big) are **handled nicely**.

---

## 📂 Project Structure

```
image-gallery/
│
├── index.php       (upload form + show gallery)
├── upload.php      (handle file upload)
├── uploads/        (folder for images)
```

---

## 1. Upload Form + Gallery (index.php)

```php
<!doctype html>
<html>
<head>
  <title>Simple Image Gallery</title>
</head>
<body>
  <h1>Image Gallery</h1>

  <!-- Upload Form -->
  <form action="upload.php" method="post" enctype="multipart/form-data">
    <input type="file" name="image" required>
    <button type="submit">Upload</button>
  </form>
  <hr>

  <h2>Gallery:</h2>
  <?php
  $dir = "uploads/";

  if (is_dir($dir)) {
      $files = array_diff(scandir($dir), ['.', '..']);
      if (count($files) == 0) {
          echo "<p>No images uploaded yet.</p>";
      } else {
          foreach ($files as $file) {
              echo "<img src='$dir$file' width='150' style='margin:10px;'>";
          }
      }
  } else {
      echo "<p>Uploads folder not found.</p>";
  }
  ?>
</body>
</html>
```

---

## 2. Upload Handler (upload.php)

```php
<?php
try {
    if (!isset($_FILES['image'])) {
        throw new Exception("No file uploaded.");
    }

    $file = $_FILES['image'];
    $allowedTypes = ['image/jpeg', 'image/png', 'image/gif'];
    $maxSize = 2 * 1024 * 1024; // 2MB

    if ($file['error'] !== UPLOAD_ERR_OK) {
        throw new Exception("Upload error!");
    }

    if ($file['size'] > $maxSize) {
        throw new Exception("File too large. Max 2MB.");
    }

    $finfo = new finfo(FILEINFO_MIME_TYPE);
    $mime = $finfo->file($file['tmp_name']);
    if (!in_array($mime, $allowedTypes)) {
        throw new Exception("Only JPG, PNG, GIF allowed.");
    }

    // Make uploads folder if missing
    $uploadDir = "uploads/";
    if (!is_dir($uploadDir)) {
        mkdir($uploadDir);
    }

    // Give file a unique name
    $ext = pathinfo($file['name'], PATHINFO_EXTENSION);
    $newName = uniqid() . "." . $ext;

    if (!move_uploaded_file($file['tmp_name'], $uploadDir . $newName)) {
        throw new Exception("Failed to move uploaded file.");
    }

    header("Location: index.php");
    exit;
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
?>
```

---

## 🎯 How this uses the 4 concepts

1. **Form Handling** → Form with `enctype="multipart/form-data"`.
2. **File Handling** → Save and read files from the `uploads/` folder.
3. **Error Handling** → Check file type, size, and upload errors with `try...catch`.
4. **File Upload** → `move_uploaded_file()` moves images safely.

---

## ✅ Exercise Ideas

1. Show the **filename and upload date** under each image.
2. Allow deleting images (add a delete button).
3. Only allow **5 uploads per user** (track with a counter).
4. Add a **CSS grid layout** to make it look like a real gallery.
