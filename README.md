class Task:
    def __init__(self, Plant_title, description, Current_status, available_date):
        self.Plant_title = Plant_title
        self.description = description
        self.Current_status = Current_status
        self.available_date = available_date

    def __str__(self):
        return f"ID: {self.id} | Title: {self.Plant_title} | Status: {self.Current_status} | Due Date: {self.available_date}"

class TaskManager:
    def __init__(self):
        self.tasks = {}
        self.next_id = 1

    def create_task(self, Plant_title, description, Current_status, available_date):
        task = Task(Plant_title, description, Current_status, available_date)
        task.id = self.next_id
        self.tasks[self.next_id] = task
        self.next_id += 1
        return f"Task {task.id} created successfully!"

    def read_all_tasks(self):
        if not self.tasks:
            print("No tasks available.")
        for task in self.tasks.values():
            print(task)

    def read_task(self, task_id):
        try:
            task_id = int(task_id)
        except ValueError:
            print("Invalid input.")
            return

        task = self.tasks.get(task_id)
        if task:
            print(task)
        else:
            print(f"Task with ID {task_id} not found.")

    def update_task(self, task_id, Plant_title=None, description=None, Current_status=None, available_date=None):
        try:
            task_id = int(task_id)
        except ValueError:
            print("Invalid input.")
            return

        task = self.tasks.get(task_id)
        if task:
            if Plant_title:
                task.Plant_title = Plant_title
            if description:
                task.description = description
            if Current_status:
                task.Current_status = Current_status
            if available_date:
                task.available_date = available_date

            print(f"Task {task_id} updated successfully!")
        else:
            print(f"Task with ID {task_id} not found.")

    def delete_task(self, task_id):
        try:
            task_id = int(task_id)
        except ValueError:
            print("Invalid input.")
            return

        if task_id in self.tasks:
            del self.tasks[task_id]
            print(f"Task {task_id} deleted successfully!")
        else:
            print(f"Task with ID {task_id} not found.")


manager = TaskManager()

print(manager.create_task("Pathos Plant", "fast-growing houseplant", "Out of stock", "12-08-2025"))
print(manager.create_task("Lantana White", "drought-tolerant flowering shrub", "In stock", "12-08-2025"))
print(manager.create_task("Rubber plant", "a popular houseplant", "Out of stock", "12-08-2025"))

print(manager.read_all_tasks())

print(manager.update_task(3, Current_status="in stock", available_date=" "))
print(manager.read_task(3))

print(manager.read_all_tasks())

print(manager.delete_task(1))
print(manager.read_all_tasks())
