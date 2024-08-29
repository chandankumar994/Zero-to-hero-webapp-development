### **Day-wise Training Plan for HTML + CSS + JavaScript**

This plan will guide you from basic to advanced concepts over a span of 21 days, covering HTML, CSS, and JavaScript. Each day includes a brief description, topics covered, and example code snippets.

---

### **Week 1: HTML & CSS Basics**

#### **Day 1: Introduction to HTML**
- **Topics:**
  - What is HTML?
  - Basic structure of an HTML document.
  - Common HTML tags: `<html>`, `<head>`, `<title>`, `<body>`, `<h1>` to `<h6>`, `<p>`, `<a>`, `<img>`, `<div>`, `<span>`.
- **Example Code:**
  ```html
  <!DOCTYPE html>
  <html>
  <head>
      <title>My First Web Page</title>
  </head>
  <body>
      <h1>Welcome to My Website</h1>
      <p>This is a paragraph.</p>
      <a href="https://www.example.com">Visit Example</a>
  </body>
  </html>
  ```

#### **Day 2: Lists, Tables, and Forms**
- **Topics:**
  - Creating ordered and unordered lists.
  - Defining tables and understanding table elements (`<table>`, `<tr>`, `<td>`, `<th>`, `<thead>`, `<tbody>`, `<tfoot>`).
  - Building basic forms with input elements (`<input>`, `<textarea>`, `<button>`, `<select>`, `<option>`).
- **Example Code:**
  ```html
  <ul>
      <li>Item 1</li>
      <li>Item 2</li>
      <li>Item 3</li>
  </ul>

  <table>
      <thead>
          <tr>
              <th>Name</th>
              <th>Age</th>
          </tr>
      </thead>
      <tbody>
          <tr>
              <td>John</td>
              <td>30</td>
          </tr>
      </tbody>
  </table>

  <form action="/submit">
      <label for="name">Name:</label>
      <input type="text" id="name" name="name">
      <button type="submit">Submit</button>
  </form>
  ```

#### **Day 3: Introduction to CSS**
- **Topics:**
  - What is CSS?
  - Different ways to apply CSS: inline, internal, and external styles.
  - Basic selectors and properties (color, font-size, background-color, margin, padding, etc.).
- **Example Code:**
  ```html
  <style>
      body {
          background-color: lightblue;
      }
      h1 {
          color: navy;
          font-family: Arial, sans-serif;
      }
      p {
          font-size: 14px;
      }
  </style>
  ```

#### **Day 4: Box Model & Positioning**
- **Topics:**
  - Understanding the CSS box model: content, padding, border, margin.
  - Different types of positioning: static, relative, absolute, fixed.
  - Using `display` and `float` for layout.
- **Example Code:**
  ```html
  <style>
      .box {
          width: 200px;
          padding: 20px;
          border: 2px solid black;
          margin: 10px;
      }
      .container {
          position: relative;
      }
      .child {
          position: absolute;
          top: 50px;
          left: 50px;
      }
  </style>

  <div class="box">This is a box.</div>
  <div class="container">
      <div class="child">Positioned Box</div>
  </div>
  ```

#### **Day 5: Responsive Design & Flexbox**
- **Topics:**
  - Introduction to responsive design principles.
  - Media queries.
  - Introduction to Flexbox and its properties.
- **Example Code:**
  ```html
  <style>
      .container {
          display: flex;
          justify-content: space-around;
      }
      .box {
          flex: 1;
          margin: 10px;
          padding: 20px;
          border: 1px solid #000;
      }

      @media (max-width: 600px) {
          .container {
              flex-direction: column;
          }
      }
  </style>

  <div class="container">
      <div class="box">Box 1</div>
      <div class="box">Box 2</div>
      <div class="box">Box 3</div>
  </div>
  ```

#### **Day 6: CSS Grid**
- **Topics:**
  - Introduction to CSS Grid.
  - Creating complex layouts using Grid.
  - Understanding grid tracks, areas, and auto-placement.
- **Example Code:**
  ```html
  <style>
      .grid-container {
          display: grid;
          grid-template-columns: auto auto auto;
          gap: 10px;
      }
      .grid-item {
          padding: 20px;
          border: 1px solid #000;
          text-align: center;
      }
  </style>

  <div class="grid-container">
      <div class="grid-item">1</div>
      <div class="grid-item">2</div>
      <div class="grid-item">3</div>
      <div class="grid-item">4</div>
      <div class="grid-item">5</div>
      <div class="grid-item">6</div>
  </div>
  ```

#### **Day 7: CSS Transitions & Animations**
- **Topics:**
  - Adding transitions to CSS properties.
  - Creating simple CSS animations.
  - Using keyframes to define animation sequences.
- **Example Code:**
  ```html
  <style>
      .box {
          width: 100px;
          height: 100px;
          background-color: red;
          transition: background-color 0.5s ease;
      }
      .box:hover {
          background-color: blue;
      }

      @keyframes move {
          from {transform: translateX(0);}
          to {transform: translateX(100px);}
      }

      .animated-box {
          width: 100px;
          height: 100px;
          background-color: green;
          animation: move 2s infinite alternate;
      }
  </style>

  <div class="box">Hover over me</div>
  <div class="animated-box">I move!</div>
  ```

---

### **Week 2: JavaScript Basics**

#### **Day 8: Introduction to JavaScript**
- **Topics:**
  - What is JavaScript?
  - Embedding JavaScript in HTML.
  - Basic syntax, variables, and data types.
  - Using `console.log` for debugging.
- **Example Code:**
  ```html
  <script>
      var name = "John Doe";
      console.log("Hello, " + name);
  </script>
  ```

#### **Day 9: JavaScript Operators & Control Structures**
- **Topics:**
  - Arithmetic, comparison, logical, and assignment operators.
  - Conditional statements (`if`, `else if`, `else`, `switch`).
  - Loops (`for`, `while`, `do...while`).
- **Example Code:**
  ```html
  <script>
      var number = 10;

      // Conditional statement
      if (number > 0) {
          console.log("Number is positive");
      } else {
          console.log("Number is non-positive");
      }

      // Loop
      for (var i = 0; i < 5; i++) {
          console.log("i = " + i);
      }
  </script>
  ```

#### **Day 10: Functions & Events**
- **Topics:**
  - Defining and invoking functions.
  - Event handling in JavaScript.
  - Understanding `onclick`, `onload`, and other event attributes.
- **Example Code:**
  ```html
  <script>
      function greet() {
          alert("Hello, welcome to the site!");
      }
  </script>

  <button onclick="greet()">Click me</button>
  ```

#### **Day 11: DOM Manipulation**
- **Topics:**
  - Understanding the Document Object Model (DOM).
  - Selecting and manipulating HTML elements with JavaScript.
  - Changing content, styles, and attributes dynamically.
- **Example Code:**
  ```html
  <script>
      function changeText() {
          document.getElementById("myParagraph").innerHTML = "Text changed!";
      }
  </script>

  <p id="myParagraph">This is a paragraph.</p>
  <button onclick="changeText()">Change Text</button>
  ```

#### **Day 12: Arrays & Objects**
- **Topics:**
  - Creating and manipulating arrays.
  - Introduction to objects and object properties.
  - Iterating over arrays and objects.
- **Example Code:**
  ```html
  <script>
      var fruits = ["Apple", "Banana", "Cherry"];
      console.log("First fruit: " + fruits[0]);

      var person = {
          firstName: "John",
          lastName: "Doe",
          age: 30
      };
      console.log(person.firstName + " " + person.lastName);
  </script>
  ```

#### **Day 13: JSON & AJAX**
- **

Topics:**
  - Understanding JSON format.
  - Parsing and stringifying JSON data.
  - Introduction to AJAX and making asynchronous requests.
- **Example Code:**
  ```html
  <script>
      var jsonString = '{"name": "John", "age": 30}';
      var obj = JSON.parse(jsonString);
      console.log(obj.name); // Output: John

      // AJAX Example
      var xhr = new XMLHttpRequest();
      xhr.open("GET", "https://jsonplaceholder.typicode.com/posts/1", true);
      xhr.onreadystatechange = function() {
          if (xhr.readyState == 4 && xhr.status == 200) {
              console.log(JSON.parse(xhr.responseText));
          }
      };
      xhr.send();
  </script>
  ```

#### **Day 14: JavaScript ES6+ Features**
- **Topics:**
  - Introduction to ES6 and beyond.
  - Let and const, arrow functions, template literals, destructuring.
  - Understanding promises and async/await.
- **Example Code:**
  ```html
  <script>
      // Let and Const
      const name = "Jane Doe";
      let age = 25;

      // Arrow Function
      const greet = () => console.log("Hello, " + name);

      // Template Literal
      console.log(`Name: ${name}, Age: ${age}`);

      // Promise Example
      const myPromise = new Promise((resolve, reject) => {
          setTimeout(() => resolve("Success!"), 2000);
      });

      myPromise.then(result => console.log(result));
  </script>
  ```

---

### **Week 3: Advanced Concepts & Project**

#### **Day 15: CSS Preprocessors (Sass)**
- **Topics:**
  - Introduction to CSS preprocessors.
  - Basic Sass syntax: variables, nesting, and mixins.
  - Compiling Sass to CSS.
- **Example Code (Sass):**
  ```scss
  $primary-color: #333;

  body {
      color: $primary-color;

      .container {
          padding: 20px;
          background-color: lighten($primary-color, 20%);
      }
  }
  ```

#### **Day 16: JavaScript Frameworks Overview**
- **Topics:**
  - Introduction to JavaScript frameworks (React, Angular, Vue).
  - Basics of working with frameworks.
  - Choosing the right framework for your project.
- **No Example Code:** (Focus on theory and framework setup)

#### **Day 17: API Integration**
- **Topics:**
  - Understanding RESTful APIs.
  - Making GET and POST requests using fetch API.
  - Handling API responses and errors.
- **Example Code:**
  ```html
  <script>
      // Fetch API Example
      fetch('https://jsonplaceholder.typicode.com/posts')
          .then(response => response.json())
          .then(data => console.log(data))
          .catch(error => console.error('Error:', error));
  </script>
  ```

#### **Day 18: Web Storage & Local Storage**
- **Topics:**
  - Introduction to web storage: localStorage and sessionStorage.
  - Storing, retrieving, and deleting data in local storage.
  - Practical use cases.
- **Example Code:**
  ```html
  <script>
      // Store data
      localStorage.setItem("username", "john_doe");

      // Retrieve data
      var username = localStorage.getItem("username");
      console.log(username); // Output: john_doe

      // Delete data
      localStorage.removeItem("username");
  </script>
  ```

#### **Day 19: Webpack & Module Bundling**
- **Topics:**
  - Introduction to module bundling and Webpack.
  - Setting up a basic Webpack project.
  - Importing and exporting modules in JavaScript.
- **Example Code (Webpack):**
  ```javascript
  // src/index.js
  import { greet } from './greet';

  greet();

  // src/greet.js
  export function greet() {
      console.log('Hello, Webpack!');
  }
  ```

#### **Day 20: Progressive Web Apps (PWA)**
- **Topics:**
  - Introduction to PWAs.
  - Creating a manifest file.
  - Service workers and offline capabilities.
  - Converting a web app into a PWA.
- **Example Code (Manifest):**
  ```json
  {
      "name": "My PWA",
      "short_name": "PWA",
      "start_url": "/index.html",
      "display": "standalone",
      "background_color": "#ffffff",
      "theme_color": "#000000",
      "icons": [
          {
              "src": "icon.png",
              "sizes": "192x192",
              "type": "image/png"
          }
      ]
  }
  ```

#### **Day 21: Final Project**
- **Topics:**
  - Build a small, responsive web application using HTML, CSS, and JavaScript.
  - Integrate API data, handle user interactions, and make the app PWA ready.
  - Example project ideas: To-Do list, Weather app, or Portfolio site.

- **Example Code Snippet:**
  ```html
  <!-- Structure for a To-Do List app -->
  <div id="app">
      <h1>To-Do List</h1>
      <input type="text" id="new-task" placeholder="New task">
      <button onclick="addTask()">Add</button>
      <ul id="task-list"></ul>
  </div>

  <script>
      function addTask() {
          const taskInput = document.getElementById("new-task");
          const taskList = document.getElementById("task-list");

          if (taskInput.value.trim() !== "") {
              const li = document.createElement("li");
              li.textContent = taskInput.value;
              taskList.appendChild(li);
              taskInput.value = "";
          }
      }
  </script>
  ```

---

This plan progressively builds your skills in HTML, CSS, and JavaScript, leading to the creation of a comprehensive web application by the end of the course. Each day's topic is designed to build upon the previous day's lessons, ensuring a solid understanding of web development.
