# driver-expense
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="A simple to-do list application with local storage functionality">
    <meta name="theme-color" content="#007bff">
    <title>My To-Do List - Task Manager</title>
    <link rel="stylesheet" href="css/style.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body>
    <div class="container">
        <!-- Header -->
        <header class="header">
            <div class="header-content">
                <div class="header-left">
                    <h1><i class="fas fa-tasks"></i> My To-Do List</h1>
                </div>
                <div class="header-right">
                    <button id="themeToggle" class="theme-toggle" title="Toggle Dark Mode">
                        <i class="fas fa-moon"></i>
                    </button>
                </div>
            </div>
        </header>

        <!-- Main Content -->
        <main class="main-content">
            <!-- Input Section -->
            <section class="input-section">
                <div class="input-wrapper">
                    <input 
                        type="text" 
                        id="taskInput" 
                        class="task-input" 
                        placeholder="Add a new task..."
                        autocomplete="off"
                    >
                    <button id="addBtn" class="add-btn" title="Add Task">
                        <i class="fas fa-plus"></i>
                    </button>
                </div>
            </section>

            <!-- Filter and Stats Section -->
            <section class="filter-stats-section">
                <div class="filter-buttons">
                    <button class="filter-btn active" data-filter="all">
                        <i class="fas fa-list"></i> All
                    </button>
                    <button class="filter-btn" data-filter="active">
                        <i class="fas fa-circle"></i> Active
                    </button>
                    <button class="filter-btn" data-filter="completed">
                        <i class="fas fa-check-circle"></i> Completed
                    </button>
                </div>

                <div class="stats-display">
                    <div class="stat">
                        <span class="stat-label">Total:</span>
                        <span class="stat-value" id="totalTasks">0</span>
                    </div>
                    <div class="stat">
                        <span class="stat-label">Active:</span>
                        <span class="stat-value" id="activeTasks">0</span>
                    </div>
                    <div class="stat">
                        <span class="stat-label">Completed:</span>
                        <span class="stat-value" id="completedTasks">0</span>
                    </div>
                </div>
            </section>

            <!-- Tasks List Section -->
            <section class="tasks-section">
                <ul id="taskList" class="task-list">
                    <!-- Tasks will be inserted here by JavaScript -->
                </ul>

                <!-- Empty State -->
                <div id="emptyState" class="empty-state">
                    <i class="fas fa-inbox"></i>
                    <p>No tasks yet!</p>
                    <small>Add a new task to get started</small>
                </div>
            </section>

            <!-- Action Buttons Section -->
            <section class="action-section">
                <button id="clearCompleted" class="btn btn-danger" title="Clear completed tasks">
                    <i class="fas fa-trash-alt"></i> Clear Completed
                </button>
                <button id="clearAll" class="btn btn-warning" title="Clear all tasks">
                    <i class="fas fa-broom"></i> Clear All
                </button>
            </section>
        </main>

        <!-- Footer -->
        <footer class="footer">
            <p>&copy; 2024 My To-Do List App | Built with <i class="fas fa-heart"></i> using HTML, CSS & JavaScript</p>
            <p class="storage-info">📦 Tasks are stored locally in your browser</p>
        </footer>
    </div>

    <!-- Toast Notification -->
    <div id="toast" class="toast"></div>

    <script src="js/app.js"></script>
</body>
</html>
/* ==========================================
   CSS Variables & Root Styles
   ========================================== */

:root {
    --primary-color: #007bff;
    --primary-dark: #0056b3;
    --success-color: #28a745;
    --danger-color: #dc3545;
    --warning-color: #ffc107;
    --info-color: #17a2b8;
    --light-color: #f8f9fa;
    --dark-color: #343a40;
    --border-color: #dee2e6;
    --text-color: #212529;
    --text-light: #6c757d;
    --shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    --shadow-lg: 0 4px 16px rgba(0, 0, 0, 0.15);
    --transition: all 0.3s ease;
    --border-radius: 8px;
}

/* Dark Mode Variables */
body.dark-mode {
    --primary-color: #0d6efd;
    --light-color: #212529;
    --dark-color: #f8f9fa;
    --text-color: #f8f9fa;
    --text-light: #adb5bd;
    --border-color: #495057;
}

/* ==========================================
   Global Styles
   ========================================== */

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

html {
    scroll-behavior: smooth;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh;
    color: var(--text-color);
    background-attachment: fixed;
    transition: var(--transition);
}

body.dark-mode {
    background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
}

/* ==========================================
   Container & Layout
   ========================================== */

.container {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
    display: flex;
    flex-direction: column;
    min-height: 100vh;
}

/* ==========================================
   Header
   ========================================== */

.header {
    background: white;
    border-radius: var(--border-radius);
    padding: 25px;
    margin-bottom: 25px;
    box-shadow: var(--shadow-lg);
    transition: var(--transition);
}

body.dark-mode .header {
    background: #2d3748;
    box-shadow: 0 4px 16px rgba(0, 0, 0, 0.3);
}

.header-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.header-left h1 {
    font-size: 2.5rem;
    color: var(--primary-color);
    display: flex;
    align-items: center;
    gap: 15px;
    margin: 0;
}

.header-left h1 i {
    color: var(--primary-color);
}

/* Theme Toggle Button */
.theme-toggle {
    background: var(--light-color);
    border: 2px solid var(--border-color);
    color: var(--text-color);
    width: 50px;
    height: 50px;
    border-radius: 50%;
    cursor: pointer;
    font-size: 1.3rem;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: var(--transition);
}

.theme-toggle:hover {
    background: var(--primary-color);
    color: white;
    border-color: var(--primary-color);
    transform: scale(1.1);
}

.theme-toggle:active {
    transform: scale(0.95);
}

/* ==========================================
   Main Content
   ========================================== */

.main-content {
    flex: 1;
}

/* ==========================================
   Input Section
   ========================================== */

.input-section {
    background: white;
    padding: 20px;
    border-radius: var(--border-radius);
    margin-bottom: 20px;
    box-shadow: var(--shadow-lg);
    transition: var(--transition);
}

body.dark-mode .input-section {
    background: #2d3748;
}

.input-wrapper {
    display: flex;
    gap: 10px;
    width: 100%;
}

.task-input {
    flex: 1;
    padding: 15px;
    border: 2px solid var(--border-color);
    border-radius: var(--border-radius);
    font-size: 1rem;
    color: var(--text-color);
    background: var(--light-color);
    transition: var(--transition);
}

body.dark-mode .task-input {
    background: #374151;
    border-color: #495057;
}

.task-input:focus {
    outline: none;
    border-color: var(--primary-color);
    box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.25);
}

.task-input::placeholder {
    color: var(--text-light);
}

.add-btn {
    padding: 15px 30px;
    background: var(--primary-color);
    color: white;
    border: none;
    border-radius: var(--border-radius);
    font-size: 1rem;
    cursor: pointer;
    transition: var(--transition);
    font-weight: 600;
    display: flex;
    align-items: center;
    justify-content: center;
    min-width: 60px;
}

.add-btn:hover {
    background: var(--primary-dark);
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0, 123, 255, 0.4);
}

.add-btn:active {
    transform: translateY(0);
}

/* ==========================================
   Filter and Stats Section
   ========================================== */

.filter-stats-section {
    background: white;
    padding: 20px;
    border-radius: var(--border-radius);
    margin-bottom: 20px;
    box-shadow: var(--shadow-lg);
    transition: var(--transition);
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 20px;
}

body.dark-mode .filter-stats-section {
    background: #2d3748;
}

.filter-buttons {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
}

.filter-btn {
    padding: 10px 16px;
    background: var(--light-color);
    border: 2px solid var(--border-color);
    color: var(--text-color);
    border-radius: var(--border-radius);
    cursor: pointer;
    transition: var(--transition);
    font-weight: 500;
    display: flex;
    align-items: center;
    gap: 8px;
}

body.dark-mode .filter-btn {
    background: #374151;
    border-color: #495057;
}

.filter-btn:hover {
    border-color: var(--primary-color);
    color: var(--primary-color);
}

.filter-btn.active {
    background: var(--primary-color);
    color: white;
    border-color: var(--primary-color);
}

.stats-display {
    display: flex;
    gap: 25px;
    justify-content: flex-end;
}

.stat {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.stat-label {
    font-size: 0.9rem;
    color: var(--text-light);
    font-weight: 500;
}

.stat-value {
    font-size: 1.5rem;
    font-weight: bold;
    color: var(--primary-color);
}

/* ==========================================
   Tasks Section
   ========================================== */

.tasks-section {
    background: white;
    border-radius: var(--border-radius);
    padding: 20px;
    margin-bottom: 20px;
    box-shadow: var(--shadow-lg);
    transition: var(--transition);
    min-height: 200px;
}

body.dark-mode .tasks-section {
    background: #2d3748;
}

.task-list {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 12px;
}

/* ==========================================
   Task Item
   ========================================== */

.task-item {
    display: flex;
    align-items: center;
    gap: 15px;
    padding: 15px;
    background: var(--light-color);
    border-radius: var(--border-radius);
    border-left: 4px solid var(--primary-color);
    transition: var(--transition);
    animation: slideIn 0.3s ease;
}

body.dark-mode .task-item {
    background: #374151;
}

@keyframes slideIn {
    from {
        opacity: 0;
        transform: translateX(-20px);
    }
    to {
        opacity: 1;
        transform: translateX(0);
    }
}

.task-item:hover {
    box-shadow: var(--shadow-lg);
    transform: translateX(5px);
}

.task-item.completed {
    opacity: 0.7;
}

.task-item.completed .task-text {
    text-decoration: line-through;
    color: var(--text-light);
}

/* Checkbox */
.task-checkbox {
    width: 24px;
    height: 24px;
    cursor: pointer;
    accent-color: var(--success-color);
}

/* Task Text */
.task-text {
    flex: 1;
    font-size: 1rem;
    color: var(--text-color);
    word-break: break-word;
    transition: var(--transition);
}

.task-text.editing {
    display: none;
}

/* Edit Input */
.task-edit-input {
    flex: 1;
    padding: 8px 12px;
    border: 2px solid var(--primary-color);
    border-radius: 4px;
    font-size: 1rem;
    color: var(--text-color);
    background: var(--light-color);
    display: none;
}

body.dark-mode .task-edit-input {
    background: #495057;
}

.task-item.is-editing .task-text.editing,
.task-item.is-editing .task-edit-input {
    display: block;
}

.task-item.is-editing .task-text:not(.editing),
.task-item.is-editing .task-edit-input:not([style*="display: block"]) {
    display: none;
}

.task-edit-input:focus {
    outline: none;
    box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.25);
}

/* Task Metadata */
.task-meta {
    font-size: 0.8rem;
    color: var(--text-light);
    white-space: nowrap;
}

/* Action Buttons */
.task-actions {
    display: flex;
    gap: 8px;
}

.task-btn {
    width: 36px;
    height: 36px;
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: var(--transition);
    font-size: 0.9rem;
}

.task-btn.edit {
    background: var(--info-color);
    color: white;
}

.task-btn.edit:hover {
    background: #117a8b;
    transform: scale(1.1);
}

.task-btn.delete {
    background: var(--danger-color);
    color: white;
}

.task-btn.delete:hover {
    background: #bd2130;
    transform: scale(1.1);
}

.task-btn.save {
    background: var(--success-color);
    color: white;
}

.task-btn.save:hover {
    background: #1e7e34;
}

.task-btn.cancel {
    background: var(--warning-color);
    color: #000;
}

.task-btn.cancel:hover {
    background: #ffb800;
}

/* ==========================================
   Empty State
   ========================================== */

.empty-state {
    display: none;
    text-align: center;
    padding: 60px 20px;
    color: var(--text-light);
}

.empty-state.show {
    display: block;
}

.empty-state i {
    font-size: 4rem;
    color: var(--border-color);
    margin-bottom: 15px;
    opacity: 0.5;
}

.empty-state p {
    font-size: 1.3rem;
    font-weight: 500;
    margin-bottom: 8px;
}

.empty-state small {
    font-size: 0.9rem;
    color: var(--text-light);
}

/* ==========================================
   Action Section
   ========================================== */

.action-section {
    display: flex;
    gap: 12px;
    margin-bottom: 20px;
    flex-wrap: wrap;
}

.btn {
    padding: 12px 20px;
    border: none;
    border-radius: var(--border-radius);
    cursor: pointer;
    font-size: 0.95rem;
    font-weight: 600;
    transition: var(--transition);
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    flex: 1;
    min-width: 150px;
}

.btn-danger {
    background: var(--danger-color);
    color: white;
}

.btn-danger:hover {
    background: #bd2130;
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(220, 53, 69, 0.4);
}

.btn-warning {
    background: var(--warning-color);
    color: #000;
}

.btn-warning:hover {
    background: #ffb800;
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(255, 193, 7, 0.4);
}

.btn:disabled {
    opacity: 0.5;
    cursor: not-allowed;
    transform: none;
}

/* ==========================================
   Footer
   ========================================== */

.footer {
    background: rgba(255, 255, 255, 0.95);
    color: var(--text-color);
    text-align: center;
    padding: 20px;
    border-radius: var(--border-radius);
    margin-top: auto;
    font-size: 0.9rem;
    box-shadow: var(--shadow-lg);
    transition: var(--transition);
}

body.dark-mode .footer {
    background: rgba(45, 55, 72, 0.95);
    color: var(--text-color);
}

.footer p {
    margin: 8px 0;
}

.footer i {
    color: var(--danger-color);
}

.storage-info {
    font-size: 0.85rem;
    color: var(--text-light);
}

/* ==========================================
   Toast Notification
   ========================================== */

.toast {
    position: fixed;
    bottom: -100px;
    left: 50%;
    transform: translateX(-50%);
    background: #333;
    color: white;
    padding: 15px 25px;
    border-radius: var(--border-radius);
    box-shadow: var(--shadow-lg);
    transition: bottom 0.3s ease;
    z-index: 1000;
    max-width: 90%;
    word-wrap: break-word;
}

.toast.show {
    bottom: 30px;
}

.toast.success {
    background: var(--success-color);
}

.toast.error {
    background: var(--danger-color);
}

.toast.info {
    background: var(--info-color);
}

/* ==========================================
   Responsive Design
   ========================================== */

@media (max-width: 768px) {
    .container {
        padding: 10px;
    }

    .header-left h1 {
        font-size: 1.8rem;
    }

    .filter-stats-section {
        flex-direction: column;
        align-items: stretch;
    }

    .stats-display {
        justify-content: space-around;
        width: 100%;
    }

    .filter-buttons {
        width: 100%;
        justify-content: space-between;
    }

    .task-item {
        flex-wrap: wrap;
    }

    .task-text {
        flex-basis: 100%;
    }

    .task-actions {
        width: 100%;
        justify-content: flex-end;
    }

    .task-meta {
        flex-basis: 100%;
    }

    .action-section {
        flex-direction: column;
    }

    .btn {
        width: 100%;
        min-width: unset;
    }
}

@media (max-width: 480px) {
    .header-left h1 {
        font-size: 1.5rem;
    }

    .header-left h1 i {
        display: none;
    }

    .task-input {
        font-size: 16px;
    }

    .task-btn {
        width: 32px;
        height: 32px;
    }

    .stats-display {
        gap: 15px;
    }

    .stat-value {
        font-size: 1.2rem;
    }
}

@media (prefers-reduced-motion: reduce) {
    * {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
    }
}

@media (prefers-color-scheme: dark) {
    body:not(.light-mode) {
        background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
    }

    body:not(.light-mode) {
        color: #f8f9fa;
    }
}

@media print {
    body {
        background: white;
    }

    .header,
    .input-section,
    .filter-stats-section,
    .action-section,
    .footer,
    .theme-toggle,
    .task-actions {
        display: none;
    }

    .task-item {
        page-break-inside: avoid;
    }
}/* ==========================================
   TO-DO LIST APPLICATION
   JavaScript Core Logic
   ========================================== */

// Task Management Class
class TodoApp {
    constructor() {
        this.tasks = [];
        this.currentFilter = 'all';
        this.init();
    }

    // Initialize the app
    init() {
        this.setupElements();
        this.setupEventListeners();
        this.loadTasks();
        this.initTheme();
        this.render();
    }

    // Setup DOM elements
    setupElements() {
        this.taskInput = document.getElementById('taskInput');
        this.addBtn = document.getElementById('addBtn');
        this.taskList = document.getElementById('taskList');
        this.emptyState = document.getElementById('emptyState');
        this.themeToggle = document.getElementById('themeToggle');
        this.clearCompletedBtn = document.getElementById('clearCompleted');
        this.clearAllBtn = document.getElementById('clearAll');
        this.totalTasksEl = document.getElementById('totalTasks');
        this.activeTasksEl = document.getElementById('activeTasks');
        this.completedTasksEl = document.getElementById('completedTasks');
        this.filterButtons = document.querySelectorAll('.filter-btn');
        this.toast = document.getElementById('toast');
    }

    // Setup event listeners
    setupEventListeners() {
        // Add task events
        this.addBtn.addEventListener('click', () => this.addTask());
        this.taskInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') this.addTask();
        });

        // Clear buttons
        this.clearCompletedBtn.addEventListener('click', () => this.clearCompleted());
        this.clearAllBtn.addEventListener('click', () => this.clearAll());

        // Theme toggle
        this.themeToggle.addEventListener('click', () => this.toggleTheme());

        // Filter buttons
        this.filterButtons.forEach(btn => {
            btn.addEventListener('click', (e) => {
                this.currentFilter = e.target.closest('.filter-btn').dataset.filter;
                this.updateFilterButtons();
                this.render();
            });
        });
    }

    // Add a new task
    addTask() {
        const text = this.taskInput.value.trim();

        if (!text) {
            this.showToast('Please enter a task!', 'error');
            return;
        }

        const task = {
            id: Date.now(),
            text: text,
            completed: false,
            createdAt: new Date().toISOString(),
            updatedAt: new Date().toISOString()
        };

        this.tasks.unshift(task);
        this.taskInput.value = '';
        this.taskInput.focus();
        this.saveTasks();
        this.render();
        this.showToast('Task added successfully!', 'success');
    }

    // Delete a task
    deleteTask(id) {
        if (confirm('Are you sure you want to delete this task?')) {
            const taskIndex = this.tasks.findIndex(t => t.id === id);
            if (taskIndex !== -1) {
                const deletedTask = this.tasks.splice(taskIndex, 1)[0];
                this.saveTasks();
                this.render();
                this.showToast(`"${deletedTask.text}" deleted`, 'info');
            }
        }
    }

    // Toggle task completion
    toggleTask(id) {
        const task = this.tasks.find(t => t.id === id);
        if (task) {
            task.completed = !task.completed;
            task.updatedAt = new Date().toISOString();
            this.saveTasks();
            this.render();
        }
    }

    // Edit a task
    editTask(id) {
        const taskEl = document.querySelector(`[data-task-id="${id}"]`);
        if (taskEl) {
            taskEl.classList.add('is-editing');
            const input = taskEl.querySelector('.task-edit-input');
            input.value = input.value || taskEl.querySelector('.task-text').textContent;
            input.focus();
            input.select();

            // Save on Enter
            const saveHandler = (e) => {
                if (e.key === 'Enter') this.saveEdit(id);
                if (e.key === 'Escape') this.cancelEdit(id);
            };

            input.addEventListener('keydown', saveHandler);

            // Add save and cancel buttons event listeners
            const saveBtn = taskEl.querySelector('.save');
            const cancelBtn = taskEl.querySelector('.cancel');

            saveBtn.onclick = () => this.saveEdit(id);
            cancelBtn.onclick = () => this.cancelEdit(id);
        }
    }

    // Save edited task
    saveEdit(id) {
        const taskEl = document.querySelector(`[data-task-id="${id}"]`);
        const input = taskEl.querySelector('.task-edit-input');
        const newText = input.value.trim();

        if (!newText) {
            this.showToast('Task cannot be empty!', 'error');
            return;
        }

        const task = this.tasks.find(t => t.id === id);
        if (task) {
            task.text = newText;
            task.updatedAt = new Date().toISOString();
            this.saveTasks();
            this.render();
            this.showToast('Task updated!', 'success');
        }
    }

    // Cancel editing
    cancelEdit(id) {
        const taskEl = document.querySelector(`[data-task-id="${id}"]`);
        if (taskEl) {
            taskEl.classList.remove('is-editing');
            this.render();
        }
    }

    // Clear all completed tasks
    clearCompleted() {
        const completedCount = this.tasks.filter(t => t.completed).length;

        if (completedCount === 0) {
            this.showToast('No completed tasks to clear!', 'info');
            return;
        }

        if (confirm(`Delete ${completedCount} completed task(s)?`)) {
            this.tasks = this.tasks.filter(t => !t.completed);
            this.saveTasks();
            this.render();
            this.showToast(`${completedCount} task(s) cleared!`, 'success');
        }
    }

    // Clear all tasks
    clearAll() {
        if (this.tasks.length === 0) {
            this.showToast('No tasks to clear!', 'info');
            return;
        }

        if (confirm('Delete ALL tasks? This cannot be undone!')) {
            this.tasks = [];
            this.saveTasks();
            this.render();
            this.showToast('All tasks cleared!', 'success');
        }
    }

    // Filter tasks based on current filter
    getFilteredTasks() {
        switch (this.currentFilter) {
            case 'active':
                return this.tasks.filter(t => !t.completed);
            case 'completed':
                return this.tasks.filter(t => t.completed);
            default:
                return this.tasks;
        }
    }

    // Update task statistics
    updateStats() {
        const total = this.tasks.length;
        const completed = this.tasks.filter(t => t.completed).length;
        const active = total - completed;

        this.totalTasksEl.textContent = total;
        this.activeTasksEl.textContent = active;
        this.completedTasksEl.textContent = completed;
    }

    // Update filter button active state
    updateFilterButtons() {
        this.filterButtons.forEach(btn => {
            btn.classList.toggle('active', btn.dataset.filter === this.currentFilter);
        });
    }

    // Render the UI
    render() {
        const filteredTasks = this.getFilteredTasks();
        this.taskList.innerHTML = '';

        if (filteredTasks.length === 0) {
            this.emptyState.classList.add('show');
        } else {
            this.emptyState.classList.remove('show');
            filteredTasks.forEach(task => {
                this.taskList.appendChild(this.createTaskElement(task));
            });
        }

        this.updateStats();
    }

    // Create task list item element
    createTaskElement(task) {
        const li = document.createElement('li');
        li.className = `task-item ${task.completed ? 'completed' : ''}`;
        li.dataset.taskId = task.id;

        const createdDate = new Date(task.createdAt).toLocaleDateString();

        li.innerHTML = `
            <input 
                type="checkbox" 
                class="task-checkbox" 
                ${task.completed ? 'checked' : ''}
                onchange="app.toggleTask(${task.id})"
            >
            <span class="task-text">${this.escapeHtml(task.text)}</span>
            <input 
                type="text" 
                class="task-edit-input" 
                value="${this.escapeHtml(task.text)}"
            >
            <span class="task-meta">${createdDate}</span>
            <div class="task-actions">
                <button class="task-btn edit" onclick="app.editTask(${task.id})" title="Edit task">
                    <i class="fas fa-edit"></i>
                </button>
                <button class="task-btn save" onclick="app.saveEdit(${task.id})" title="Save task" style="display: none;">
                    <i class="fas fa-check"></i>
                </button>
                <button class="task-btn cancel" onclick="app.cancelEdit(${task.id})" title="Cancel edit" style="display: none;">
                    <i class="fas fa-times"></i>
                </button>
                <button class="task-btn delete" onclick="app.deleteTask(${task.id})" title="Delete task">
                    <i class="fas fa-trash"></i>
                </button>
            </div>
        `;

        return li;
    }

    // Escape HTML to prevent XSS
    escapeHtml(text) {
        const div = document.createElement('div');
        div.textContent = text;
        return div.innerHTML;
    }

    // Save tasks to localStorage
    saveTasks() {
        try {
            localStorage.setItem('todoTasks', JSON.stringify(this.tasks));
        } catch (error) {
            console.error('Error saving tasks:', error);
            this.showToast('Error saving tasks!', 'error');
        }
    }

    // Load tasks from localStorage
    loadTasks() {
        try {
            const saved = localStorage.getItem('todoTasks');
            this.tasks = saved ? JSON.parse(saved) : [];
        } catch (error) {
            console.error('Error loading tasks:', error);
            this.tasks = [];
            this.showToast('Error loading tasks!', 'error');
        }
    }

    // Initialize theme
    initTheme() {
        const savedTheme = localStorage.getItem('todoTheme');
        const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;

        if (savedTheme === 'dark' || (!savedTheme && prefersDark)) {
            document.body.classList.add('dark-mode');
            this.updateThemeIcon();
        }
    }

    // Toggle theme
    toggleTheme() {
        document.body.classList.toggle('dark-mode');
        const isDark = document.body.classList.contains('dark-mode');
        localStorage.setItem('todoTheme', isDark ? 'dark' : 'light');
        this.updateThemeIcon();
        this.showToast(`Switched to ${isDark ? 'dark' : 'light'} mode!`, 'info');
    }

    // Update theme icon
    updateThemeIcon() {
        const isDark = document.body.classList.contains('dark-mode');
        this.themeToggle.innerHTML = isDark 
            ? '<i class="fas fa-sun"></i>' 
            : '<i class="fas fa-moon"></i>';
    }

    // Show toast notification
    showToast(message, type = 'info') {
        this.toast.textContent = message;
        this.toast.className = `toast ${type} show`;

        setTimeout(() => {
            this.toast.classList.remove('show');
        }, 3000);
    }
}

// Initialize app when DOM is loaded
document.addEventListener('DOMContentLoaded', () => {
    window.app = new TodoApp();
});

// Keyboard shortcut hints
document.addEventListener('keydown', (e) => {
    // Ctrl/Cmd + Enter to add task from anywhere
    if ((e.ctrlKey || e.metaKey) && e.key === 'Enter') {
        if (document.activeElement === app.taskInput) {
            app.addTask();
        }
    }
});
