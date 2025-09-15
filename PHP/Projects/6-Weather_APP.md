# 🌦 Weather Forecast App with City Search (Core PHP + OpenWeatherMap)

👉 Save this as `weather.php`

```php
<?php
// ---------------------------
// Weather Forecast App in PHP
// ---------------------------

// Your OpenWeatherMap API Key (replace with your own)
$apiKey = "YOUR_API_KEY";

// Default city if user has not searched yet
$city = "Delhi,IN";

// If user searched for a city
if (isset($_GET['city']) && !empty($_GET['city'])) {
    $city = $_GET['city'];
}

// Step 1: Get latitude & longitude for city
$geoUrl = "http://api.openweathermap.org/geo/1.0/direct?q=" . urlencode($city) . "&limit=1&appid=$apiKey";
$geoResponse = file_get_contents($geoUrl);
$geoData = json_decode($geoResponse, true);

// Handle invalid city
if (empty($geoData)) {
    $error = "❌ City not found. Please try again.";
} else {
    $lat = $geoData[0]['lat'];
    $lon = $geoData[0]['lon'];

    // Step 2: Get 7-day forecast
    $apiUrl = "https://api.openweathermap.org/data/2.5/onecall?lat=$lat&lon=$lon&exclude=current,minutely,hourly,alerts&units=metric&appid=$apiKey";
    $response = file_get_contents($apiUrl);
    $data = json_decode($response, true);
}
?>
<!DOCTYPE html>
<html>
<head>
    <title>7-Day Weather Forecast</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body class="bg-light">
<div class="container mt-5">
    <h2 class="mb-4 text-center">🌦 Weather Forecast App</h2>

    <!-- Search Form -->
    <form method="GET" action="" class="mb-4">
        <div class="row justify-content-center">
            <div class="col-md-6">
                <input type="text" name="city" class="form-control" placeholder="Enter city name (e.g., London,IN)" value="<?php echo htmlspecialchars($city); ?>">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary w-100">Search</button>
            </div>
        </div>
    </form>

    <?php if (isset($error)) { ?>
        <div class="alert alert-danger text-center"><?php echo $error; ?></div>
    <?php } elseif (isset($data)) { ?>
        <h4 class="mb-4 text-center">7-Day Forecast for <span class="text-primary"><?php echo htmlspecialchars($city); ?></span></h4>
        <div class="row">
            <?php
            foreach ($data['daily'] as $index => $day) {
                if ($index == 7) break; // Show only 7 days
                $date = date("l, d M Y", $day['dt']);
                $tempDay = $day['temp']['day'];
                $tempNight = $day['temp']['night'];
                $weather = $day['weather'][0]['main'];
                $icon = $day['weather'][0]['icon'];
            ?>
            <div class="col-md-3 mb-3">
                <div class="card text-center shadow-sm">
                    <div class="card-body">
                        <h6><?php echo $date; ?></h6>
                        <img src="http://openweathermap.org/img/wn/<?php echo $icon; ?>@2x.png" alt="Weather icon">
                        <p class="mb-1"><strong><?php echo $weather; ?></strong></p>
                        <p class="mb-0">🌞 Day: <?php echo $tempDay; ?> °C</p>
                        <p>🌙 Night: <?php echo $tempNight; ?> °C</p>
                    </div>
                </div>
            </div>
            <?php } ?>
        </div>
    <?php } ?>
</div>
</body>
</html>
```

---

## ✅ Features

* Search for **any city** (e.g., `London`, `New York`, `Mumbai`).
* Displays **7-day forecast** with weather icons.
* Error message if city not found.
* Clean layout with Bootstrap.

---

⚡ Try it:

1. Replace `YOUR_API_KEY` with your OpenWeatherMap API key.
2. Open `http://localhost/weather.php`
3. Enter any city and see the forecast.


---

## 🛠 Steps to Get OpenWeatherMap API Key

1. Go to 👉 [https://openweathermap.org/](https://openweathermap.org/)
2. Click **Sign Up** (top right).
3. Fill in your details (name, email, password).
4. After confirming your email, **Log in**.
5. In your profile → go to **API Keys**.

   * Direct link: [https://home.openweathermap.org/api\_keys](https://home.openweathermap.org/api_keys)
6. You’ll see a **default key** (usually named *default*).

   * Example: `abc123def456ghi789`
7. Copy this key and replace in your PHP code:

```php
$apiKey = "YOUR_API_KEY"; // Replace with your key
```

---

## ⚠️ Important Notes

* It may take **10–15 minutes** after sign-up for the key to start working.
* The **free plan** allows:
  ✅ Current weather
  ✅ 7-day forecast (One Call API)
  ✅ 60 calls per minute (more than enough for practice)

---
