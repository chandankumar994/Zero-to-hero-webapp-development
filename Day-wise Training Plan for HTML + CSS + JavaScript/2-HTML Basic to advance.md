Here’s a day-wise training plan for learning HTML, from basic concepts to more advanced topics:

---

### **Week 1: Introduction to HTML**

#### **Day 1: Introduction to HTML**
- **Topics:**
  - What is HTML?
  - Basic structure of an HTML document.
  - HTML tags and elements.
  - Creating your first HTML page.

- **Example Code:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>My First HTML Page</title>
  </head>
  <body>
      <h1>Hello, World!</h1>
      <p>This is my first HTML page.</p>
  </body>
  </html>
  ```

#### **Day 2: Working with Text**
- **Topics:**
  - Paragraphs and headings.
  - Bold, italic, and underline text.
  - Lists: ordered and unordered.
  - Text alignment and spacing.

- **Example Code:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Text Formatting</title>
  </head>
  <body>
      <h1>Main Heading</h1>
      <h2>Subheading</h2>
      <p>This is a paragraph of text. <strong>Bold text</strong>, <em>italic text</em>, and <u>underlined text</u>.</p>
      <ul>
          <li>Item 1</li>
          <li>Item 2</li>
          <li>Item 3</li>
      </ul>
      <ol>
          <li>First Item</li>
          <li>Second Item</li>
          <li>Third Item</li>
      </ol>
  </body>
  </html>
  ```

#### **Day 3: Links and Images**
- **Topics:**
  - Creating hyperlinks.
  - Linking to external sites and internal pages.
  - Adding images to your page.
  - Image attributes: alt, width, height.

- **Example Code:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Links and Images</title>
  </head>
  <body>
      <h1>Links and Images</h1>
      <p>Visit <a href="https://www.example.com">Example Website</a>.</p>
      <p>Go to <a href="page2.html">Page 2</a>.</p>
      <img src="https://via.placeholder.com/150" alt="Placeholder Image">
  </body>
  </html>
  ```

#### **Day 4: Tables**
- **Topics:**
  - Creating basic tables.
  - Table rows, columns, and cells.
  - Table headers and captions.
  - Merging cells: colspan and rowspan.

- **Example Code:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>HTML Tables</title>
  </head>
  <body>
      <h1>HTML Tables</h1>
      <table border="1">
          <caption>Student Grades</caption>
          <tr>
              <th>Name</th>
              <th>Subject</th>
              <th>Grade</th>
          </tr>
          <tr>
              <td>Alice</td>
              <td>Math</td>
              <td>A</td>
          </tr>
          <tr>
              <td>Bob</td>
              <td>Science</td>
              <td>B+</td>
          </tr>
      </table>
  </body>
  </html>
  ```

#### **Day 5: Forms**
- **Topics:**
  - Creating a basic HTML form.
  - Form elements: input, textarea, select, and button.
  - Form attributes: action, method, and input types.
  - Grouping form elements with fieldsets.

- **Example Code:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>HTML Forms</title>
  </head>
  <body>
      <h1>Contact Form</h1>
      <form action="/submit" method="post">
          <label for="name">Name:</label>
          <input type="text" id="name" name="name"><br><br>
          
          <label for="email">Email:</label>
          <input type="email" id="email" name="email"><br><br>
          
          <label for="message">Message:</label><br>
          <textarea id="message" name="message"></textarea><br><br>
          
          <button type="submit">Submit</button>
      </form>
  </body>
  </html>
  ```

#### **Day 6: Semantic HTML**
- **Topics:**
  - Understanding semantic HTML elements.
  - Using `<header>`, `<footer>`, `<nav>`, `<article>`, `<section>`, and `<aside>`.
  - Importance of semantic HTML for accessibility and SEO.

- **Example Code:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Semantic HTML</title>
  </head>
  <body>
      <header>
          <h1>My Website</h1>
          <nav>
              <ul>
                  <li><a href="#">Home</a></li>
                  <li><a href="#">About</a></li>
                  <li><a href="#">Contact</a></li>
              </ul>
          </nav>
      </header>
      
      <section>
          <h2>Main Content</h2>
          <article>
              <h3>Article Title</h3>
              <p>This is an article about a specific topic.</p>
          </article>
      </section>
      
      <aside>
          <h2>Related Links</h2>
          <ul>
              <li><a href="#">Link 1</a></li>
              <li><a href="#">Link 2</a></li>
          </ul>
      </aside>
      
      <footer>
          <p>&copy; 2024 My Website</p>
      </footer>
  </body>
  </html>
  ```

#### **Day 7: Multimedia**
- **Topics:**
  - Embedding videos and audio files.
  - Using `<video>` and `<audio>` elements.
  - Adding controls, autoplay, and loop attributes.
  - Embedding YouTube videos.

- **Example Code:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Multimedia in HTML</title>
  </head>
  <body>
      <h1>Embedding Multimedia</h1>
      
      <h2>Video Example</h2>
      <video width="320" height="240" controls>
          <source src="movie.mp4" type="video/mp4">
          Your browser does not support the video tag.
      </video>
      
      <h2>Audio Example</h2>
      <audio controls>
          <source src="audio.mp3" type="audio/mpeg">
          Your browser does not support the audio element.
      </audio>
      
      <h2>YouTube Video</h2>
      <iframe width="560" height="315" src="https://www.youtube.com/embed/dQw4w9WgXcQ" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
  </body>
  </html>
  ```

---

### **Week 2: Intermediate HTML**

#### **Day 8: HTML Entities and Special Characters**
- **Topics:**
  - Understanding HTML entities.
  - Commonly used entities: `&nbsp;`, `&amp;`, `&copy;`, `&lt;`, `&gt;`.
  - Using entities for special characters.

- **Example Code:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>HTML Entities</title>
  </head>
  <body>
      <p>Use &amp; to represent an ampersand (&).</p>
      <p>Use &lt; and &gt; to represent less than (&lt;) and greater than (&gt;).</p>
      <p>Use &copy; to represent the copyright symbol (&copy; 2024).</p>
  </body>
  </html>
  ```

#### **Day 9: Iframes and Embeds**
- **Topics:**
  - Embedding other web pages using `<iframe>`.
  - Adding content from external sources (maps, videos).
  - Attributes of iframe: src, width, height, frameborder.

- **Example Code:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Iframes and Embeds</title>
  </head>
  <body>
      <h1>Iframes Example</h1>
      <iframe src="https://www.example.com" width="600" height="400" frameborder="0"></iframe>
      
      <h1>Embedded Google Map</h1>
      <iframe
          width="600"
          height="450"
          style="border:0"
          loading="lazy"
          allowfullscreen
          referrerpolicy="no-referrer-when-downgrade"
          src="https://www.google.com/maps/embed/v1/place?key=YOUR_API_KEY&q=Eiffel+Tower,Paris+France">
      </iframe>
  </body>
  </html>
  ```

#### **Day 10: Block vs Inline Elements**
- **Topics:**
  - Understanding block-level and inline elements.
  - Examples of block elements (`<div>`, `<p>`, `<h1>`, etc.).
  - Examples of inline elements (`<span>`, `<a>`, `<img>`, etc.).
  - How block and inline elements affect layout.

- **Example Code:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Block vs Inline Elements</title>
  </head>
  <body>
      <div style="border: 1px solid black; padding: 10px;">
          <h1>This is a Block Element</h1>
          <p>This paragraph is also a block element.</p>
          <span>This is an inline element inside a paragraph.</span>
      </div>
  </body>
  </html>
  ```

#### **Day 11: Meta Tags and SEO Basics**
- **Topics:**
  - Using meta tags for SEO.
  - Common meta tags: charset, viewport, description, keywords, author.
  - Importance of meta descriptions and keywords.
  - Using Open Graph meta tags for social media.

- **Example Code:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta name="description" content="This is a sample website for learning HTML.">
      <meta name="keywords" content="HTML, CSS, JavaScript">
      <meta name="author" content="Your Name">
      <title>Meta Tags and SEO</title>
  </head>
  <body>
      <h1>Understanding Meta Tags</h1>
      <p>Check the HTML source to see the meta tags in action.</p>
  </body>
  </html>
  ```

#### **Day 12: HTML5 Forms**
- **Topics:**
  - New input types in HTML5: date, email, range, color, etc.
  - Form validation with HTML5 attributes.
  - Placeholder text, required fields, and pattern matching.
  - Using `<datalist>` for autocomplete.

- **Example Code:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>HTML5 Forms</title>
  </head>
  <body>
      <h1>HTML5 Form Elements</h1>
      <form action="/submit" method="post">
          <label for="birthday">Birthday:</label>
          <input type="date" id="birthday" name="birthday"><br><br>

          <label for="email">Email:</label>
          <input type="email" id="email" name="email" required><br><br>

          <label for="color">Favorite Color:</label>
          <input type="color" id="color" name="color"><br><br>

          <label for="range">Volume:</label>
          <input type="range" id="range" name="range" min="0" max="10"><br><br>

          <label for="browser">Choose your browser:</label>
          <input list="browsers" id="browser" name="browser">
          <datalist id="browsers">
              <option value="Chrome">
              <option value="Firefox">
              <option value="Safari">
              <option value="Edge">
          </datalist><br><br>

          <button type="submit">Submit</button>
      </form>
  </body>
  </html>
  ```

#### **Day 13: Responsive Web Design Basics**
- **Topics:**
  - Introduction to responsive design.
  - Using the viewport meta tag.
  - Media queries for different screen sizes.
  - Responsive images and videos.

- **Example Code:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Responsive Design</title>
      <style>
          body {
              font-family: Arial, sans-serif;
              margin: 0;
              padding: 0;
          }

          .container {
              max-width: 1200px;
              margin: 0 auto;
              padding: 10px;
          }

          .box {
              width: 100%;
              padding: 20px;
              background-color: lightblue;
              margin: 10px 0;
          }

          @media (min-width: 600px) {
              .box {
                  width: 48%;
                  float: left;
                  margin: 1%;
              }
          }
      </style>
  </head>
  <body>
      <div class="container">
          <div class="box">Box 1</div>
          <div class="box">Box 2</div>
          <div class="box">Box 3</div>
          <div class="box">Box 4</div>
      </div>
  </body>
  </html>
  ```

#### **Day 14: Project 1 - Building a Simple Portfolio**
- **Topics:**
  - Review of what has been learned so far.
  - Create a simple portfolio website using the concepts covered.
  - Structure the project with multiple pages: Home, About, Portfolio, and Contact.
  - Focus on clean and semantic HTML structure, proper use of forms, tables, and multimedia.

- **Example Project Structure:**
  - **index.html**: Home page.
  - **about.html**: About me page.
  - **portfolio.html**: Showcase your projects.
  - **contact.html**: Contact form.

- **Example Code for Home Page:**
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
          <h1>Welcome to My Portfolio</h1>
      </header>
      
      <nav>
          <ul>
              <li><a href="index.html">Home</a></li>
              <li><a href="about.html">About Me</a></li>
              <li><a href="portfolio.html">Portfolio</a></li>
              <li><a href="contact.html">Contact</a></li>
          </ul>
      </nav>
      
      <section>
          <h2>About This Site</h2>
          <p>This is my personal portfolio website where I showcase my skills and projects.</p>
      </section>
      
      <footer>
          <p>&copy; 2024 My Portfolio</p>
      </footer>
  </body>
  </html>
  ```

---

This plan covers the fundamentals of HTML over the course of two weeks. Each day builds on the previous day's knowledge, gradually introducing more complex topics. The end goal is to create a fully functional and responsive portfolio website using the concepts learned.
