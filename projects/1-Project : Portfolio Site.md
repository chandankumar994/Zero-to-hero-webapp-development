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
