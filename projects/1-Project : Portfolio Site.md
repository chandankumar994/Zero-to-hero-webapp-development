Here are step-by-step guides to create three different projects: a Portfolio site, a To-Do list, and a Weather app. Each project will progressively build on your knowledge of HTML, CSS, and JavaScript.

---

### **Project 1: Portfolio Site**

#### **1. Project Overview**
Create a personal portfolio website that showcases your projects, skills, and contact information. This project will focus on HTML and CSS, with some JavaScript for interactivity.

#### **2. Structure**
- **Home (index.html)**
  - Header with navigation links (Home, About, Projects, Contact).
  - Introduction section with a personal photo and a short bio.
  - Projects section with thumbnails and descriptions.
  - Contact section with a form to send messages.

- **About (about.html)**
  - Detailed bio with education, experience, and skills.

- **Projects (projects.html)**
  - A gallery of your work, each with a title, description, and link to the live project or GitHub repo.

- **Contact (contact.html)**
  - A contact form with fields for name, email, subject, and message.

#### **3. Example Code**

**index.html**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Portfolio</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <nav>
            <ul>
                <li><a href="index.html">Home</a></li>
                <li><a href="about.html">About</a></li>
                <li><a href="projects.html">Projects</a></li>
                <li><a href="contact.html">Contact</a></li>
            </ul>
        </nav>
    </header>

    <section id="home">
        <h1>Welcome to My Portfolio</h1>
        <p>Hello! I'm a web developer with a passion for creating beautiful and functional websites.</p>
    </section>

    <section id="projects">
        <h2>My Projects</h2>
        <div class="project">
            <h3>Project 1</h3>
            <p>Description of Project 1.</p>
        </div>
        <div class="project">
            <h3>Project 2</h3>
            <p>Description of Project 2.</p>
        </div>
    </section>

    <footer>
        <p>&copy; 2024 My Portfolio</p>
    </footer>
</body>
</html>
```

**styles.css**
```css
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f4f4f4;
}

header {
    background-color: #333;
    color: #fff;
    padding: 10px 0;
}

header nav ul {
    list-style: none;
    display: flex;
    justify-content: center;
}

header nav ul li {
    margin: 0 15px;
}

header nav ul li a {
    color: #fff;
    text-decoration: none;
}

section {
    padding: 20px;
}

h1, h2 {
    text-align: center;
}

#projects .project {
    margin: 20px 0;
    padding: 10px;
    background-color: #fff;
    border: 1px solid #ccc;
}

footer {
    text-align: center;
    padding: 10px;
    background-color: #333;
    color: #fff;
}
```

---

### **Project 2: To-Do List**

#### **1. Project Overview**
Create a simple To-Do list application where users can add tasks, mark them as complete, and delete them.

#### **2. Structure**
- **index.html**
  - Input field for adding a new task.
  - Button to add the task to the list.
  - Unordered list to display tasks.
  - Each task has a checkbox to mark as complete and a delete button.

#### **3. Example Code**

**index.html**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div id="app">
        <h1>To-Do List</h1>
        <input type="text" id="new-task" placeholder="New task">
        <button id="add-task">Add</button>
        <ul id="task-list"></ul>
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

#task-list {
    list-style: none;
    padding: 0;
}

#task-list li {
    display: flex;
    justify-content: space-between;
    padding: 5px 0;
    border-bottom: 1px solid #ccc;
}

#task-list li.completed {
    text-decoration: line-through;
    color: #888;
}
```

**script.js**
```javascript
document.getElementById('add-task').addEventListener('click', function() {
    var taskText = document.getElementById('new-task').value;
    if (taskText.trim() !== '') {
        var li = document.createElement('li');
        var checkbox = document.createElement('input');
        checkbox.type = 'checkbox';
        checkbox.addEventListener('change', function() {
            if (checkbox.checked) {
                li.classList.add('completed');
            } else {
                li.classList.remove('completed');
            }
        });
        li.appendChild(checkbox);
        li.appendChild(document.createTextNode(taskText));
        var deleteBtn = document.createElement('button');
        deleteBtn.textContent = 'Delete';
        deleteBtn.addEventListener('click', function() {
            li.remove();
        });
        li.appendChild(deleteBtn);
        document.getElementById('task-list').appendChild(li);
        document.getElementById('new-task').value = '';
    }
});
```

---

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
