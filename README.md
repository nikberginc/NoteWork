# NoteWork 📝

**Completed:** August  4, 2025

A command-line task management application built with Python. NoteWork allows users to create, rename, organize, and delete tasks, with the additional ability to schedule time-based reminders.

I developed this project at age 16 after one school year of learning programming with Raptor, as a way to further develop my Python programming skills and experiment with task management and background timers.

## Features

- **Task creation:** Add tasks with custom names.
- **Task management:** View, rename, and delete existing tasks.
- **Time-based reminders:** Set a specific hour and minute for a task reminder.
- **Background timers:** Uses Python threading to monitor scheduled reminders while the application remains usable.
- **Input validation:** Prevents duplicate task names and checks time inputs.
- **Task deletion:** Delete individual tasks or clear the entire task list.
- **Menu navigation:** Return to the main menu without saving unfinished changes.
- **Exit command:** Close the application using the `exit` command at supported prompts.

## Requirements

- Python 3
- No additional libraries required.

The application uses Python's built-in modules:

- `threading`
- `time`
- `datetime`

## Getting Started

1. Download `NoteWork.py` from this repository.
2. Open a terminal in the folder containing the Python file.
3. Run the following command:

   ```bash
   python NoteWork.py
   ```

4. Read the instructions and type `Start` to begin using the application.

## How to Use

After starting the program, the main menu displays your current tasks and allows you to select an action.

### 1. Adding a Task

Type `Add task` in the main menu.

The program will ask you to enter a name for your new task.

You can then choose whether to assign a reminder:

- Type `Time` to configure a reminder.
- Enter anything else to add the task without a reminder.

If you select a reminder, enter the desired hour (0–23) and minute (0–59).

**Example:**

```text
How would you like to name this task?
Finish homework

If you want to add time to your new task type Time
Time

Enter hour (0-23): 18
Enter minute (0-59): 30

⏳ Timer set for task Finish homework at 18:30.
```

When the scheduled time is reached, the application displays:

```text
⏰ Time is up for task: Finish homework
```

If the selected time has already passed, the reminder is scheduled for the following day.

### 2. Renaming a Task

Type `Rename` in the main menu.

Enter the name of the existing task, followed by its new name.

The program checks whether the task exists and prevents duplicate names.

If the task has a scheduled reminder, its entry in the active timer dictionary is updated to use the new name.

### 3. Deleting Tasks

Type `Delete` in the main menu.

You can:

- Enter a task's name to delete that specific task.
- Enter `All` to clear the entire task list.

Deleting an individual task also attempts to cancel its associated reminder.

**Note:** The current implementation has a limitation when deleting all tasks, described below.

### 4. Navigation Commands

| Command | Function |
|---|---|
| `Start` | Start the application after the introduction |
| `Add task` | Create a new task |
| `Rename` | Rename an existing task |
| `Delete` | Delete one or all tasks |
| `Time` | Add a reminder while creating a task |
| `All` | Delete all tasks in the deletion menu |
| `Menu` | Return to the main menu at supported prompts |
| `Exit` | Close the application at supported prompts |

Commands are case-insensitive, but spaces and wording must be entered correctly.

## How It Works

NoteWork combines several fundamental Python programming concepts.

### Task Storage

Tasks are stored in a Python list:

```python
task_list = []
```

The program uses list operations such as `append()`, `remove()`, and `index()` to manage tasks.

### Reminder System

Scheduled reminders are managed using Python's `threading` and `datetime` modules.

Each reminder runs in a separate daemon thread, allowing the main application to continue accepting commands.

A dictionary stores cancellation events associated with task names:

```python
active_timers = {}
```

The reminder thread periodically compares the current time against the scheduled time.

When the target time is reached, the application prints a notification in the terminal.

### Input Validation

The program uses loops, conditional statements, and exception handling to validate user input.

For example, it checks that reminder hours are between 0 and 23 and minutes are between 0 and 59.

### Program Structure

The application uses a continuous `while True` loop to display the task list and allow users to perform different actions.

Temporary variables are used during task creation to prevent unfinished tasks from being added when the user returns to the main menu.

## Known Limitations

- **No permanent storage:** Tasks and reminders are stored in memory and are lost when the application closes.
- **No graphical interface:** The application operates entirely through the terminal.
- **No completed-task status:** Marking tasks as completed is not implemented in the current version.
- **Reminder precision:** Reminder threads check the current time approximately every 10 seconds, so notifications may appear slightly late.
- **Delete-all behavior:** Clearing all tasks removes entries from the active timer dictionary but does not cancel the already-running reminder threads.
- **Renamed reminders:** Renaming a task updates its dictionary entry, but an existing reminder can still display the original task name.
- **No desktop notifications:** Reminders are printed in the terminal rather than displayed as operating-system notifications.

## Development Note

NoteWork was developed as a personal Python programming project to practice working with lists, loops, conditional statements, functions, input validation, and task management.

The reminder functionality was developed with some assistance from ChatGPT, particularly for implementing background threads and scheduling reminders.


**Author:** [Nik Berginc](https://github.com/nikberginc)
