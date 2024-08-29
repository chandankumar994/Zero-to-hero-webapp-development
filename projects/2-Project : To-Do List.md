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
