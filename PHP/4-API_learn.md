# API tutorial demo

We’ll cover:

1. What an API is
2. How to call an API in PHP (step by step)
3. How to process JSON data
4. Example: Display user data in a Bootstrap table

---

# 🌐 PHP API Tutorial for Beginners

---

## 🔹 1. What is an API?

* **API** = Application Programming Interface.
* It allows two applications to talk to each other.
* Example: Weather app uses a weather API to get temperature info.

In our demo, we’ll use a **Free API**:
👉 `https://jsonplaceholder.typicode.com/users`
This returns fake user data (great for testing).

---

## 🔹 2. Fetch API Data in PHP using cURL

```php
<?php
// Step 1: Define API URL
$url = "https://jsonplaceholder.typicode.com/users";

// Step 2: Initialize cURL
$ch = curl_init();

// Step 3: Set options
curl_setopt($ch, CURLOPT_URL, $url);             // API URL
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true); // Return response as string
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false); // Ignore SSL certificate issues

// Step 4: Execute API request
$response = curl_exec($ch);

// Step 5: Error handling
if (curl_errno($ch)) {
    die("cURL Error: " . curl_error($ch));
}

// Step 6: Close cURL
curl_close($ch);

// Step 7: Convert JSON response into PHP array
$data = json_decode($response, true);
?>
```

---

## 🔹 3. Understanding the Response

When you call the API, it returns JSON like this:

```json
[
  {
    "id": 1,
    "name": "Leanne Graham",
    "email": "Sincere@april.biz",
    "phone": "1-770-736-8031",
    "company": { "name": "Romaguera-Crona" },
    "address": { "city": "Gwenborough" }
  },
  ...
]
```

* JSON is just structured data.
* We converted it into a **PHP array** using `json_decode()`.
* Now you can access it like:

```php
echo $data[0]['name'];   // Prints first user's name
echo $data[0]['email'];  // Prints first user's email
```

---

## 🔹 4. Display API Data in a Table

Here’s a **full working demo** with Bootstrap styling:

```php
<?php
// ========== API CALL ==========
$url = "https://jsonplaceholder.typicode.com/users";
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
$response = curl_exec($ch);
if (curl_errno($ch)) {
    die("cURL Error: " . curl_error($ch));
}
curl_close($ch);
$data = json_decode($response, true);
?>
<!DOCTYPE html>
<html>
<head>
    <title>API Demo - Users</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body class="bg-light">
<div class="container mt-5">
    <h2 class="mb-4 text-center">👨‍💻 Users Data from Free API</h2>

    <table class="table table-bordered table-striped table-hover">
        <thead class="table-dark">
            <tr>
                <th>#</th>
                <th>Name</th>
                <th>Email</th>
                <th>Phone</th>
                <th>Company</th>
                <th>City</th>
            </tr>
        </thead>
        <tbody>
            <?php
            if (is_array($data)) {
                $i = 1;
                foreach ($data as $user) {
                    echo "<tr>
                            <td>{$i}</td>
                            <td>{$user['name']}</td>
                            <td>{$user['email']}</td>
                            <td>{$user['phone']}</td>
                            <td>{$user['company']['name']}</td>
                            <td>{$user['address']['city']}</td>
                          </tr>";
                    $i++;
                }
            } else {
                echo "<tr><td colspan='6' class='text-center text-danger'>❌ Failed to load API data</td></tr>";
            }
            ?>
        </tbody>
    </table>
</div>
</body>
</html>
```

---

## 🔹 5. Practical Exercise (For You)

1. Change the API URL to:
   👉 `https://jsonplaceholder.typicode.com/posts`
   (This returns blog posts data).

2. Modify the table to show:

   * Post ID
   * Title
   * Body

This way you’ll learn how to adapt the same code to any API. 🚀

---
# Explanation: 
```php
<?php
$url = "https://jsonplaceholder.typicode.com/users";

// Initialize cURL
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);

$response = curl_exec($ch);
if (curl_errno($ch)) {
    die("cURL Error: " . curl_error($ch));
}
curl_close($ch);

$data = json_decode($response, true);
?>
```

### 1. Define the API URL

```php
$url = "https://jsonplaceholder.typicode.com/users";
```

* Here we set the API endpoint.
* This is a **fake REST API** that returns JSON with 10 user details.
* If you paste this URL in a browser, you’ll see raw JSON data.

---

### 2. Initialize cURL

```php
$ch = curl_init();
```

* cURL is a PHP library to make HTTP requests.
* `curl_init()` creates a new cURL session and stores it in `$ch`.

---

### 3. Set cURL Options

```php
curl_setopt($ch, CURLOPT_URL, $url);
```

* Tell cURL which URL to fetch (our API link).

```php
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
```

* By default, cURL **prints response directly**.
* With this option set to `true`, it **returns response as a string** → so we can store it in `$response`.

```php
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
```

* This disables SSL certificate checking.
* Normally, you should keep it `true` for security. But for beginners/testing, we set it to `false` so HTTPS calls don’t fail due to certificate issues.

---

### 4. Execute the Request

```php
$response = curl_exec($ch);
```

* Actually sends the request to the API.
* Stores the response (JSON string) into `$response`.

---

### 5. Error Handling

```php
if (curl_errno($ch)) {
    die("cURL Error: " . curl_error($ch));
}
```

* `curl_errno()` checks if there was any error (like timeout, invalid URL).
* If yes → `die()` stops the script and shows the error.

---

### 6. Close cURL

```php
curl_close($ch);
```

* Always close the session after use to free system resources.

---

### 7. Convert JSON → PHP Array

```php
$data = json_decode($response, true);
```

* The API returned JSON (string format).
* `json_decode()` converts JSON into a **PHP array** (because of `true`).
* Now `$data` is a **multi-dimensional array** of users.

Example (shortened):

```php
[
  [
    "id" => 1,
    "name" => "Leanne Graham",
    "email" => "Sincere@april.biz",
    "address" => ["city" => "Gwenborough"],
    "company" => ["name" => "Romaguera-Crona"]
  ],
  ...
]
```

---

✅ Now `$data` is ready to loop through and display in a table.

