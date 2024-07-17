### JSTodolist
### Create two variables using let and const. The let variable should be named age and set to 30. The const variable should be named name and set to "Alice". Try to reassign the name variable and observe what happens.
### AIM
Create two variables using let and const. The let variable should be named age and set to 30. The const variable should be named name and set to "Alice". Try to reassign the name variable and observe it
### PROGRAM
### todo.html
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List</title>
    <link rel="stylesheet" href="todo.css">
</head>
<body>
    <div class="container">
        <h1 style="color: black";>My To-Do List</h1>
        <p style="color: yellow";>Enter text into the input field to add items to your list.</p>
        <p style="color: greenyellow";>Click the item to mark it as complete.</p>
        <p style="color: black;">Click the "X" to remove the item from your list.</p>
        <form id="new-task-form">
            <input type="text" id="task-input" placeholder="Add a new task...">
            <button type="submit">Add</button>
        </form>
        
        <ul id="task-list"></ul>
    </div>

    <script src="todo.js"></script>
</body>
</html>

### todo.css

body {
    font-family: sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    background-color: #00bcd4;
}

.container {
    background-color: white;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

h1 {
    text-align: center;
    margin-bottom: 20px;
}

#new-task-form {
    display: flex;
}

#task-input {
    flex-grow: 1;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 3px;
    margin-right: 10px;
}

#new-task-form button {
    padding: 10px 15px;
    background-color: #4CAF50;
    color:  sky rgb(0, 255, 255);
    border: none;
    border-radius: 3px;
    cursor: pointer;
}

#task-list {
    list-style: none;
    padding: 0;
    margin-top: 20px;
}

#task-list li {
    background-color:  sky rgb(0, 255, 255);
    padding: 10px;
    border-radius: 3px;
    margin-bottom: 5px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

#task-list li input[type="checkbox"] {
    margin-right: 10px;
}

#task-list li button {
    background-color: transparent;
    border: none;
    cursor: pointer;
    font-size: 16px;
}
```
### todo.js
```
const taskInput = document.getElementById('task-input');
const newTaskForm = document.getElementById('new-task-form');
const taskList = document.getElementById('task-list');

// Task Class
class Task {
    constructor(title) {
        this.title = title;
        this.completed = false;
    }
}

// ToDoList Class
class ToDoList {
    constructor() {
        this.tasks = [];
        this.loadTasks(); // Load tasks from local storage on initialization
    }

    addTask(task) {
        this.tasks.push(task);
        this.saveTasks(); // Save the updated tasks to local storage
        this.renderTasks(); // Render the new task on the UI
    }

    deleteTask(index) {
        this.tasks.splice(index, 1);
        this.saveTasks();
        this.renderTasks();
    }

    toggleTaskCompletion(index) {
        this.tasks[index].completed = !this.tasks[index].completed;
        this.saveTasks();
        this.renderTasks();
    }

    renderTasks() {
        taskList.innerHTML = ''; // Clear the task list

        this.tasks.forEach((task, index) => {
            const li = document.createElement('li');
            li.innerHTML = `
                <input type="checkbox" ${task.completed ? 'checked' : ''} data-index="${index}">
                <span>${task.title}</span>
                <button data-index="${index}">X</button>
            `;
            taskList.appendChild(li);

            // Add event listeners to each task item
            li.querySelector('input[type="checkbox"]').addEventListener('change', () => {
                this.toggleTaskCompletion(index);
            });

            li.querySelector('button').addEventListener('click', () => {
                this.deleteTask(index);
            });
        });
    }

    // Load tasks from local storage
    loadTasks() {
        const storedTasks = JSON.parse(localStorage.getItem('tasks'));
        if (storedTasks) {
            this.tasks = storedTasks;
        }
    }

    // Save tasks to local storage
    saveTasks() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
    }
}

const toDoList = new ToDoList();

// Handle form submission
newTaskForm.addEventListener('submit', (event) => {
    event.preventDefault();
    const taskTitle = taskInput.value;
    if (taskTitle) {
        toDoList.addTask(new Task(taskTitle));
        taskInput.value = ''; // Clear the input field
    }
});

toDoList.renderTasks(); // Render initial tasks on page load
```
### OUTPUT
![day 4](https://github.com/user-attachments/assets/98400b4d-a91f-4d5a-be96-e31ec23e58a2)
### RESULT
hus the program was executed successfully.
