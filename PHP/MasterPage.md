Got it 👍 You want a **Master Page** (template) approach in **Core PHP** (without frameworks) to build a **5-page responsive health and wellness website**.

I’ll show you a clean way using `header.php`, `footer.php`, and content pages (home, about, services, blog, contact).

Here’s the full structure and sample code:

---

### 📂 Project Structure

```
health-website/
│── index.php
│── about.php
│── services.php
│── blog.php
│── contact.php
│── assets/
│    ├── css/style.css
│    └── images/
│── includes/
     ├── header.php
     └── footer.php
```

---

### ✅ `includes/header.php`

```php
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Health & Wellness</title>
  <link rel="stylesheet" href="assets/css/style.css">
</head>
<body>
  <!-- Navigation -->
  <header>
    <nav class="navbar">
      <div class="logo">Health<span>Wellness</span></div>
      <ul class="nav-links">
        <li><a href="index.php">Home</a></li>
        <li><a href="about.php">About</a></li>
        <li><a href="services.php">Services</a></li>
        <li><a href="blog.php">Blog</a></li>
        <li><a href="contact.php">Contact</a></li>
      </ul>
    </nav>
  </header>
  <main>
```

---

### ✅ `includes/footer.php`

```php
  </main>
  <footer>
    <p>&copy; <?php echo date("Y"); ?> Health & Wellness. All rights reserved.</p>
  </footer>
</body>
</html>
```

---

### ✅ `index.php` (Home Page)

```php
<?php include("includes/header.php"); ?>
<section class="hero">
  <h1>Welcome to Your Health & Wellness Journey</h1>
  <p>Eat healthy, stay active, and live a balanced life.</p>
</section>
<section class="content">
  <h2>Why Choose Us?</h2>
  <p>We provide natural diet plans, yoga guidance, and lifestyle tips tailored to your needs.</p>
</section>
<?php include("includes/footer.php"); ?>
```

---

### ✅ `about.php`

```php
<?php include("includes/header.php"); ?>
<section class="page-section">
  <h1>About Us</h1>
  <p>We are dedicated to helping individuals achieve better health through nutrition, yoga, and lifestyle changes.</p>
</section>
<?php include("includes/footer.php"); ?>
```

---

### ✅ `services.php`

```php
<?php include("includes/header.php"); ?>
<section class="page-section">
  <h1>Our Services</h1>
  <ul>
    <li>Personalized Diet Plans</li>
    <li>Yoga & Meditation Classes</li>
    <li>Wellness Workshops</li>
    <li>Holistic Health Guidance</li>
  </ul>
</section>
<?php include("includes/footer.php"); ?>
```

---

### ✅ `blog.php`

```php
<?php include("includes/header.php"); ?>
<section class="page-section">
  <h1>Health & Wellness Blog</h1>
  <article>
    <h2>5 Morning Habits for a Healthy Lifestyle</h2>
    <p>Start your day with yoga, hydration, and positivity...</p>
  </article>
  <article>
    <h2>Superfoods You Should Add to Your Diet</h2>
    <p>Discover the power of moringa, amla, turmeric, and more...</p>
  </article>
</section>
<?php include("includes/footer.php"); ?>
```

---

### ✅ `contact.php`

```php
<?php include("includes/header.php"); ?>
<section class="page-section">
  <h1>Contact Us</h1>
  <form action="#" method="post" class="contact-form">
    <input type="text" name="name" placeholder="Your Name" required>
    <input type="email" name="email" placeholder="Your Email" required>
    <textarea name="message" placeholder="Your Message" required></textarea>
    <button type="submit">Send</button>
  </form>
</section>
<?php include("includes/footer.php"); ?>
```

---

### ✅ `assets/css/style.css` (Responsive Styling)

```css
body {
  margin: 0; 
  font-family: Arial, sans-serif;
  line-height: 1.6;
}
header {
  background: #0c6b58;
  color: #fff;
  padding: 15px 20px;
}
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.logo {
  font-size: 1.5rem;
  font-weight: bold;
}
.logo span {
  color: #ffd700;
}
.nav-links {
  list-style: none;
  display: flex;
  gap: 20px;
}
.nav-links li a {
  color: #fff;
  text-decoration: none;
}
.hero {
  background: url("../images/health-bg.jpg") no-repeat center center/cover;
  color: #fff;
  text-align: center;
  padding: 100px 20px;
}
.page-section {
  padding: 40px 20px;
  max-width: 900px;
  margin: auto;
}
footer {
  text-align: center;
  background: #0c6b58;
  color: #fff;
  padding: 10px 0;
}
/* Responsive */
@media (max-width: 768px) {
  .nav-links {
    flex-direction: column;
    display: none;
  }
  .navbar.active .nav-links {
    display: flex;
  }
}
```

---

✅ This setup gives you:

* **Reusable Master Page** (header + footer)
* **5 Responsive Pages**
* **Clean CSS Layout**

---

# Send mail Enable:

---

## 1. Update `contact.php`

```php
<?php include("includes/header.php"); ?>

<section class="page-section">
  <h1>Contact Us</h1>

  <?php
  if (isset($_GET['success']) && $_GET['success'] == "1") {
      echo "<p style='color:green;'>✅ Your message has been sent successfully.</p>";
  } elseif (isset($_GET['error']) && $_GET['error'] == "1") {
      echo "<p style='color:red;'>❌ Failed to send message. Please try again.</p>";
  }
  ?>

  <form action="send_mail.php" method="post" class="contact-form">
    <input type="text" name="name" placeholder="Your Name" required>
    <input type="email" name="email" placeholder="Your Email" required>
    <textarea name="message" placeholder="Your Message" required></textarea>
    <button type="submit">Send</button>
  </form>
</section>

<?php include("includes/footer.php"); ?>
```

---

## 2. Create `send_mail.php`

```php
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $name    = htmlspecialchars(trim($_POST['name']));
    $email   = htmlspecialchars(trim($_POST['email']));
    $message = htmlspecialchars(trim($_POST['message']));

    // Replace with your email
    $to = "your-email@example.com";  
    $subject = "New Contact Form Message from $name";
    $body = "You have received a new message from your Health & Wellness website:\n\n".
            "Name: $name\n".
            "Email: $email\n\n".
            "Message:\n$message";

    $headers = "From: $email\r\n";
    $headers .= "Reply-To: $email\r\n";

    if (mail($to, $subject, $body, $headers)) {
        header("Location: contact.php?success=1");
    } else {
        header("Location: contact.php?error=1");
    }
    exit;
}
?>
```

---

## 3. Style the Contact Form (`assets/css/style.css`)

Add this at the bottom of your CSS:

```css
.contact-form {
  display: flex;
  flex-direction: column;
  gap: 15px;
  max-width: 600px;
  margin: auto;
}
.contact-form input,
.contact-form textarea {
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 1rem;
  width: 100%;
}
.contact-form button {
  background: #0c6b58;
  color: #fff;
  padding: 12px;
  border: none;
  border-radius: 8px;
  font-size: 1rem;
  cursor: pointer;
}
.contact-form button:hover {
  background: #094f40;
}
```

---

## 4. ⚠️ Important Notes

* PHP’s `mail()` works only if your hosting server has **sendmail** or an SMTP setup.
* On **local XAMPP/WAMP**, it won’t send emails directly. You’d need **SMTP configuration** (like Gmail, SendGrid, or your hosting provider’s mail server).
* If you want **reliable delivery**, I recommend using **PHPMailer** or an **SMTP API** (e.g., Gmail SMTP, SendGrid, Mailgun).

---
