### **Project 3: Weather App**

#### **1. Project Overview**
Build a weather application that fetches and displays the current weather for a specific location using a weather API.

#### **2. Structure**
- **index.html**
  - Input field to enter the city name.
  - Button to fetch weather data.
  - Display area for weather information (temperature, conditions, etc.).

#### **3. Example Code**

**index.html**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div id="app">
        <h1>Weather App</h1>
        <input type="text" id="city" placeholder="Enter city name">
        <button id="get-weather">Get Weather</button>
        <div id="weather-result"></div>
    </div>

    <script src="script.js"></script>
</body>
</html>
```

**styles.css**
```css
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

#app {
    background-color: #fff;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 8px;
    width: 300px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

#weather-result {
    margin-top: 20px;
    text-align: center;
}

#weather-result p {
    margin: 5px 0;
}
```

**script.js**
```javascript
document.getElementById('get-weather').addEventListener('click', function() {
    var city = document.getElementById('city').value;
    if (city.trim() !== '') {
        var apiKey = 'your_api_key'; // Replace with your API key
        var url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;

        fetch(url)
            .then(response => response.json())
            .then(data => {
                if (data.cod === 200) {
                    var weatherResult = `
                        <p>Temperature: ${data.main.temp}°C</p>
                        <p>Condition: ${data.weather[0].description}</

p>
                        <p>Humidity: ${data.main.humidity}%</p>
                        <p>Wind Speed: ${data.wind.speed} m/s</p>
                    `;
                    document.getElementById('weather-result').innerHTML = weatherResult;
                } else {
                    document.getElementById('weather-result').innerHTML = '<p>City not found.</p>';
                }
            })
            .catch(error => {
                console.error('Error fetching weather data:', error);
            });
    }
});
```

---

These projects are designed to give you hands-on experience with front-end web development, covering HTML, CSS, and JavaScript, and applying them in real-world scenarios. Each project builds on the previous one, helping you progressively enhance your skills.
