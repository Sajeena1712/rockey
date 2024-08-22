class Task:
    def _init_(self, description):
        self.description = description
        self.completed = False

    def mark_completed(self):
        self.completed = True

    def _str_(self):
        status = "✔" if self.completed else "✘"
        return f"[{status}] {self.description}"
    class ToDoList:
        def __init__(self):
           self.tasks = []

    def add_task(self, description):
        self.tasks.append(Task(description))

    def view_tasks(self):
        for index, task in enumerate(self.tasks, start=1):
            print(f"{index}. {task}")

    def mark_task_completed(self, index):
        if 0 <= index < len(self.tasks):
            self.tasks[index].mark_completed()

    def delete_task(self, index):
        if 0 <= index < len(self.tasks):
            self.tasks.pop(index)

    def save_tasks(self, filename):
        with open(filename, 'w') as file:
            for task in self.tasks:
                status = '1' if task.completed else '0'
                file.write(f"{status},{task.description}\n")

    def load_tasks(self, filename):
        try:
            with open(filename, 'r') as file:
                self.tasks = []
                for line in file:
                    status, description = line.strip().split(',', 1)
                    task = Task(description)
                    if status == '1':
                        task.mark_completed()
                    self.tasks.append(task)
        except FileNotFoundError:
            print(f"The file {filename} does not exist.")
    def add_task(todo_list):
        description= input("Enter task description: ")
def add_task(todo_list):
    todo_list.add_task(description) # type: ignore

def view_tasks(todo_list):
    todo_list.view_tasks()

def mark_task_completed(todo_list):
    index = int(input("Enter task number to mark as completed: ")) - 1
    todo_list.mark_task_completed(index)

def delete_task(todo_list):
    index = int(input("Enter task number to delete: ")) - 1
    todo_list.delete_task(index)

def save_and_exit(todo_list, filename):
    todo_list.save_tasks(filename)
    print("Tasks saved. Exiting.")
    exit()

def main():
    todo_list = todo_list()
    filename = "tasks.txt"

    try:
        todo_list.load_tasks(filename)
    except Exception as e:
        print(f"Error loading tasks: {e}")

    actions = {
        '1': add_task,
        '2': view_tasks,
        '3': mark_task_completed,
        '4': delete_task,
        '5': save_and_exit
    }

    while True:
        print("\n1. Add task")
        print("2. View tasks")
        print("3. Mark task as completed")
        print("4. Delete task")
        print("5. Save and exit")
        choice = input("Choose an option: ")

        action = actions.get(choice)
        if action:
            action(todo_list)
        else:
            print("Invalid choice. Please try again.")

if __name__ == "_main_":
    main()
