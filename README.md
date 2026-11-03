<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FocusFlow | Study Planner</title>

<style>
/* GENERAL DESIGN */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    background: #f7f5f0;
    color: #393a35;
}

button, input {
    font: inherit;
}

button {
    cursor: pointer;
    border: none;
}

.container {
    display: flex;
    min-height: 100vh;
}

/* SIDEBAR */
.sidebar {
    width: 230px;
    background: #efede5;
    padding: 30px 20px;
    display: flex;
    flex-direction: column;
    border-right: 1px solid #e3e0d7;
}

.logo {
    font-size: 25px;
    font-weight: bold;
    color: #68735f;
    text-align: center;
    margin-bottom: 65px;
}

.logo span {
    display: block;
    font-size: 13px;
    color: #85877d;
    font-weight: normal;
    margin-top: 5px;
}

.nav a {
    display: block;
    text-decoration: none;
    color: #55564f;
    padding: 15px;
    margin-bottom: 12px;
    border-radius: 12px;
    transition: 0.2s;
}

.nav a:hover,
.nav a.active {
    background: #dce0d2;
    color: #46513f;
}

.settings {
    margin-top: auto;
}

/* MAIN CONTENT */
.main {
    flex: 1;
    padding: 35px;
    max-width: 1500px;
    margin: auto;
}

.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 20px;
    margin-bottom: 30px;
}

.header h1 {
    font-size: 38px;
    margin-bottom: 8px;
    color: #34352f;
}

.header p {
    color: #77756e;
}

.quote {
    background: #e9dfd2;
    padding: 22px;
    border-radius: 18px;
    max-width: 350px;
    color: #62584e;
    line-height: 1.5;
    font-style: italic;
}

/* DASHBOARD GRID */
.dashboard {
    display: grid;
    grid-template-columns: 1.2fr 1fr;
    gap: 20px;
}

.card {
    background: #fffefa;
    border: 1px solid #e9e5dc;
    border-radius: 20px;
    padding: 25px;
    box-shadow: 0 3px 12px rgba(50, 45, 35, 0.03);
}

.card h2 {
    font-size: 22px;
    margin-bottom: 22px;
    color: #45463f;
}

/* TASKS */
.task-input {
    display: flex;
    gap: 8px;
    margin-bottom: 18px;
}

.task-input input {
    flex: 1;
    min-width: 0;
    padding: 13px;
    border: none;
    border-radius: 10px;
    background: #f3f0e9;
    outline: none;
}

.add-btn {
    padding: 0 18px;
    border-radius: 10px;
    background: #858e78;
    color: white;
    font-size: 22px;
}

.add-btn:hover {
    background: #68735f;
}

.task-list {
    list-style: none;
}

.task-list li {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 10px;
    padding: 14px 5px;
    border-bottom: 1px solid #eeeae2;
}

.task-left {
    display: flex;
    align-items: center;
    gap: 12px;
    min-width: 0;
}

.task-left span {
    overflow-wrap: anywhere;
}

.task-left input {
    width: 19px;
    height: 19px;
    accent-color: #858e78;
    flex-shrink: 0;
}

.completed {
    text-decoration: line-through;
    color: #aaa79f;
}

.delete-btn {
    background: transparent;
    color: #a18c7c;
    padding: 5px;
}

.progress-info {
    margin-top: 20px;
    color: #77756e;
    font-size: 14px;
}

.progress-bar {
    width: 100%;
    height: 10px;
    background: #eeeae2;
    border-radius: 20px;
    margin-top: 10px;
    overflow: hidden;
}

.progress-fill {
    width: 0%;
    height: 100%;
    background: #858e78;
    transition: 0.3s;
}

/* TIMER */
.timer-card {
    text-align: center;
}

.timer-display {
    font-size: 65px;
    font-weight: bold;
    margin: 25px 0;
    color: #34352f;
}

.timer-buttons {
    display: flex;
    justify-content: center;
    gap: 12px;
}

.timer-buttons button {
    background: #eae7df;
    color: #4d5047;
    padding: 13px 20px;
    border-radius: 50px;
}

.timer-buttons .start {
    background: #858e78;
    color: white;
}

.timer-buttons button:hover {
    opacity: 0.8;
}

.presets {
    display: flex;
    gap: 10px;
    margin-top: 28px;
}

.presets button {
    flex: 1;
    padding: 13px 5px;
    border-radius: 12px;
    background: #f2efe8;
    color: #55564f;
    border: 1px solid #e3ded3;
}

.presets button.selected {
    background: #dce0d2;
    border-color: #dce0d2;
}

/* SCHEDULE */
.schedule-item {
    display: flex;
    justify-content: space-between;
    gap: 10px;
    padding: 15px 0;
    border-bottom: 1px solid #eeeae2;
}

.schedule-item:last-child {
    border-bottom: none;
}

.schedule-item span:last-child {
    color: #858078;
    font-size: 14px;
}

/* PROGRESS */
.progress-card {
    display: flex;
    align-items: center;
    gap: 25px;
}

.progress-circle {
    width: 130px;
    height: 130px;
    border-radius: 50%;
    background: conic-gradient(
        #858e78 0%,
        #858e78 var(--progress, 0%),
        #eae7df var(--progress, 0%)
    );
    display: grid;
    place-items: center;
    flex-shrink: 0;
}

.progress-circle::before {
    content: "";
    width: 100px;
    height: 100px;
    background: #fffefa;
    border-radius: 50%;
    grid-area: 1 / 1;
}

.progress-circle strong {
    grid-area: 1 / 1;
    z-index: 1;
    font-size: 25px;
}

.progress-text h3 {
    margin-bottom: 10px;
}

.progress-text p {
    color: #858078;
    line-height: 1.5;
}

/* MOBILE DESIGN */
@media (max-width: 850px) {
    .sidebar {
        width: 180px;
    }

    .dashboard {
        grid-template-columns: 1fr;
    }

    .header {
        flex-direction: column;
        align-items: flex-start;
    }
}

@media (max-width: 600px) {
    .container {
        flex-direction: column;
    }

    .sidebar {
        width: 100%;
        padding: 15px;
    }

    .logo {
        margin-bottom: 15px;
    }

    .nav {
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
        gap: 5px;
    }

    .nav a {
        padding: 10px;
        margin: 0;
        font-size: 13px;
    }

    .settings {
        display: none;
    }

    .main {
        padding: 18px;
    }

    .header h1 {
        font-size: 30px;
    }

    .quote {
        max-width: 100%;
    }

    .card {
        padding: 18px;
    }

    .timer-display {
        font-size: 50px;
    }

    .progress-card {
        flex-direction: column;
        text-align: center;
    }
}
</style>
</head>

<body>

<div class="container">

    <!-- SIDEBAR -->
    <aside class="sidebar">
        <div class="logo">
            FocusFlow
            <span>Study smarter. Stay focused.</span>
        </div>

        <nav class="nav">
            <a href="#home" class="active">⌂ Home</a>
            <a href="#schedule">▦ Schedule</a>
            <a href="#timer">◷ Timer</a>
            <a href="#progress">▥ Progress</a>
        </nav>

        <div class="settings">
            <a href="#home">⚙ Settings</a>
        </div>
    </aside>

    <!-- MAIN CONTENT -->
    <main class="main" id="home">

        <header class="header">
            <div>
                <h1>Welcome back!</h1>
                <p>Stay focused, keep going.</p>
            </div>

            <div class="quote" id="quote">
                "A little progress each day adds up to big results."
                <br>— Unknown
            </div>
        </header>

        <div class="dashboard">

            <!-- TASK SECTION -->
            <section class="card">
                <h2>✓ My Tasks</h2>

                <div class="task-input">
                    <input
                        type="text"
                        id="taskInput"
                        placeholder="Add a new task..."
                    >
                    <button class="add-btn" onclick="addTask()">+</button>
                </div>

                <ul class="task-list" id="taskList"></ul>

                <div class="progress-info">
                    <span id="taskProgress">0 / 0 completed</span>
                    <div class="progress-bar">
                        <div class="progress-fill" id="taskBar"></div>
                    </div>
                </div>
            </section>

            <!-- TIMER SECTION -->
            <section class="card timer-card" id="timer">
                <h2>◷ Focus Timer</h2>

                <div class="timer-display" id="timerDisplay">
                    25:00
                </div>

                <div class="timer-buttons">
                    <button class="start" onclick="startTimer()">▶</button>
                    <button onclick="pauseTimer()">Ⅱ</button>
                    <button onclick="resetTimer()">↻</button>
                </div>

                <div class="presets">
                    <button class="selected" onclick="setTimer(25, this)">25 min</button>
                    <button onclick="setTimer(5, this)">5 min</button>
                    <button onclick="setTimer(15, this)">15 min</button>
                </div>
            </section>

            <!-- SCHEDULE SECTION -->
            <section class="card" id="schedule">
                <h2>▦ Study Schedule</h2>

                <div class="schedule-item">
                    <span>Math</span>
                    <span>Today, 3:00 PM</span>
                </div>

                <div class="schedule-item">
                    <span>Science</span>
                    <span>Tomorrow, 9:00 AM</span>
                </div>

                <div class="schedule-item">
                    <span>English</span>
                    <span>Tomorrow, 10:00 AM</span>
                </div>
            </section>

            <!-- PROGRESS SECTION -->
            <section class="card" id="progress">
                <h2>▥ Your Progress</h2>

                <div class="progress-card">
                    <div class="progress-circle" id="progressCircle">
                        <strong id="progressPercent">0%</strong>
                    </div>

                    <div class="progress-text">
                        <h3 id="progressMessage">You're on your way!</h3>
                        <p>Complete your tasks to see your progress grow.</p>
                    </div>
                </div>
            </section>

        </div>
    </main>
</div>

<script>
// TASK MANAGEMENT

let tasks = JSON.parse(localStorage.getItem("focusTasks")) || [];

function saveTasks() {
    localStorage.setItem("focusTasks", JSON.stringify(tasks));
}

function displayTasks() {
    const taskList = document.getElementById("taskList");
    taskList.innerHTML = "";

    tasks.forEach((task, index) => {
        const li = document.createElement("li");

        const left = document.createElement("div");
        left.className = "task-left";

        const checkbox = document.createElement("input");
        checkbox.type = "checkbox";
        checkbox.checked = task.completed;

        checkbox.onchange = () => {
            tasks[index].completed = checkbox.checked;
            saveTasks();
            displayTasks();
        };

        const name = document.createElement("span");
        name.textContent = task.name;

        if (task.completed) {
            name.classList.add("completed");
        }

        left.append(checkbox, name);

        const deleteButton = document.createElement("button");
        deleteButton.textContent = "Delete";
        deleteButton.className = "delete-btn";

        deleteButton.onclick = () => {
            tasks.splice(index, 1);
            saveTasks();
            displayTasks();
        };

        li.append(left, deleteButton);
        taskList.appendChild(li);
    });

    updateProgress();
}

function addTask() {
    const input = document.getElementById("taskInput");
    const taskName = input.value.trim();

    if (taskName === "") {
        alert("Please enter a task.");
        return;
    }

    tasks.push({
        name: taskName,
        completed: false
    });

    input.value = "";

    saveTasks();
    displayTasks();
}

document.getElementById("taskInput").addEventListener("keydown", function(event) {
    if (event.key === "Enter") {
        addTask();
    }
});

// PROGRESS TRACKING

function updateProgress() {
    const completed = tasks.filter(task => task.completed).length;
    const total = tasks.length;

    const percentage = total === 0
        ? 0
        : Math.round((completed / total) * 100);

    document.getElementById("taskProgress").textContent =
        `${completed} / ${total} completed`;

    document.getElementById("taskBar").style.width =
        percentage + "%";

    document.getElementById("progressPercent").textContent =
        percentage + "%";

    document.getElementById("progressCircle").style.setProperty(
        "--progress", percentage + "%"
    );

    let message = "You're on your way!";

    if (percentage === 100 && total > 0) {
        message = "Excellent work!";
    } else if (percentage >= 50) {
        message = "Great progress!";
    }

    document.getElementById("progressMessage").textContent = message;
}

// FOCUS TIMER

let timeLeft = 25 * 60;
let timerInterval = null;

function updateTimerDisplay() {
    const minutes = Math.floor(timeLeft / 60);
    const seconds = timeLeft % 60;

    document.getElementById("timerDisplay").textContent =
        String(minutes).padStart(2, "0") + ":" +
        String(seconds).padStart(2, "0");
}

function startTimer() {
    if (timerInterval !== null) return;

    timerInterval = setInterval(() => {
        if (timeLeft > 0) {
            timeLeft--;
            updateTimerDisplay();
        } else {
            pauseTimer();
            alert("Time is up! Take a break.");
        }
    }, 1000);
}

function pauseTimer() {
    clearInterval(timerInterval);
    timerInterval = null;
}

function resetTimer() {
    pauseTimer();
    timeLeft = 25 * 60;
    updateTimerDisplay();
}

function setTimer(minutes, button) {
    pauseTimer();

    timeLeft = minutes * 60;
    updateTimerDisplay();

    document.querySelectorAll(".presets button").forEach(btn => {
        btn.classList.remove("selected");
    });

    button.classList.add("selected");
}

// MOTIVATIONAL QUOTES

const quotes = [
    '"A little progress each day adds up to big results."',
    '"Success is the sum of small efforts repeated daily."',
    '"Focus on progress, not perfection."',
    '"Your effort today builds your future tomorrow."',
    '"Great things take time. Keep moving forward."'
];

function changeQuote() {
    const random = Math.floor(Math.random() * quotes.length);
    document.getElementById("quote").textContent = quotes[random];
}

// INITIALIZE WEBSITE

displayTasks();
updateTimerDisplay();
changeQuote();

</script>

</body>
</html>
