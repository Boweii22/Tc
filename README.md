# Tc

This exercise is about creating a simple To-Do list using HTML, CSS, and JavaScript, with the following key features:

Adding tasks using a button that opens a prompt().

Displaying tasks inside a div with the ID ft_list (new tasks go at the top).

Removing tasks when clicked, after user confirmation (confirm()).

Persisting the list using cookies so that tasks remain after refreshing or reopening the browser.



---

How You Did This

Here’s how you likely approached it using JavaScript:

1. HTML Structure (index.html)

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List</title>
    <style>
        body { text-align: center; font-family: Arial, sans-serif; }
        #ft_list { margin-top: 20px; padding: 10px; border: 1px solid #000; min-height: 100px; }
        .todo { padding: 10px; margin: 5px; background: lightgray; cursor: pointer; }
    </style>
</head>
<body>

    <button onclick="addTodo()">New</button>
    <div id="ft_list"></div>

    <script src="todo.js"></script>
</body>
</html>


---

2. JavaScript (todo.js)

// Function to get cookies
function getCookie(name) {
    let cookies = document.cookie.split('; ');
    for (let cookie of cookies) {
        let [key, value] = cookie.split('=');
        if (key === name) return decodeURIComponent(value);
    }
    return "";
}

// Function to save tasks to cookies
function saveTodos() {
    let todos = [];
    document.querySelectorAll('.todo').forEach(todo => todos.push(todo.textContent));
    document.cookie = `todos=${encodeURIComponent(JSON.stringify(todos))}; path=/`;
}

// Function to load saved tasks from cookies
function loadTodos() {
    let savedTodos = getCookie("todos");
    if (savedTodos) {
        JSON.parse(savedTodos).forEach(task => createTodo(task));
    }
}

// Function to create a new task
function createTodo(text) {
    if (!text) return;
    let div = document.createElement("div");
    div.className = "todo";
    div.textContent = text;

    div.onclick = function() {
        if (confirm("Do you want to delete this task?")) {
            div.remove();
            saveTodos();
        }
    };

    let ft_list = document.getElementById("ft_list");
    ft_list.insertBefore(div, ft_list.firstChild);
    saveTodos();
}

// Function to add a new To-Do
function addTodo() {
    let task = prompt("Enter a new TO DO:");
    if (task) createTodo(task);
}

// Load todos on page load
window.onload = loadTodos;


---

Explanation of How It Works

1. addTodo() → Opens a prompt to get a new task, then adds it at the top.


2. createTodo(text) → Creates a new <div> with the task text, adds a click event for removal, and inserts it at the top of #ft_list.


3. saveTodos() → Saves tasks to cookies in JSON format.


4. getCookie(name) → Reads cookies and returns the task list if available.


5. loadTodos() → Loads saved tasks from cookies when the page is opened.


6. Clicking a task → Opens a confirmation popup (confirm()). If confirmed, the task is deleted.




---

Improvements You Could Add

✅ Use localStorage instead of cookies for better handling of longer lists.
✅ Add a CSS animation when adding/removing tasks.
✅ Allow editing tasks instead of just deleting them.

Let me know if you need modifications or additional features! 🚀

