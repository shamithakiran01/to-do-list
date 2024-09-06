# to-do-list
this is a simple to-do -list made with the help off basic java

import java.util.ArrayList;
import java.util.Scanner;

class Task {
    String description;
    boolean isComplete;
    int priority;
    String dueDate;

    public Task(String description, int priority, String dueDate) {
        this.description = description;
        this.isComplete = false;
        this.priority = priority;
        this.dueDate = dueDate;
    }

    @Override
    public String toString() {
        return (isComplete ? "[X] " : "[ ] ") + description + " (Priority: " + priority + ", Due: " + dueDate + ")";
    }
}

public class ToDoListApp {
    private static ArrayList<Task> tasks = new ArrayList<>();

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        while (true) {
            System.out.println("\nTo-Do List Application");
            System.out.println("1. Add Task");
            System.out.println("2. Remove Task");
            System.out.println("3. Mark Task as Complete");
            System.out.println("4. View Tasks");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");
            int option = scanner.nextInt();
            scanner.nextLine();  // Consume newline

            switch (option) {
                case 1:
                    addTask(scanner);
                    break;
                case 2:
                    removeTask(scanner);
                    break;
                case 3:
                    markTaskAsComplete(scanner);
                    break;
                case 4:
                    viewTasks();
                    break;
                case 5:
                    System.out.println("Exiting...");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid option, please try again.");
            }
        }
    }

    private static void addTask(Scanner scanner) {
        System.out.print("Enter task description: ");
        String description = scanner.nextLine();
        System.out.print("Enter task priority (1-5): ");
        int priority = scanner.nextInt();
        scanner.nextLine();  // Consume newline
        System.out.print("Enter task due date (YYYY-MM-DD): ");
        String dueDate = scanner.nextLine();
        tasks.add(new Task(description, priority, dueDate));
        System.out.println("Task added.");
    }

    private static void removeTask(Scanner scanner) {
        viewTasks();
        System.out.print("Enter task number to remove: ");
        int taskNumber = scanner.nextInt();
        scanner.nextLine();  // Consume newline
        if (taskNumber >= 1 && taskNumber <= tasks.size()) {
            tasks.remove(taskNumber - 1);
            System.out.println("Task removed.");
        } else {
            System.out.println("Invalid task number.");
        }
    }

    private static void markTaskAsComplete(Scanner scanner) {
        viewTasks();
        System.out.print("Enter task number to mark as complete: ");
        int taskNumber = scanner.nextInt();
        scanner.nextLine();  // Consume newline
        if (taskNumber >= 1 && taskNumber <= tasks.size()) {
            tasks.get(taskNumber - 1).isComplete = true;
            System.out.println("Task marked as complete.");
        } else {
            System.out.println("Invalid task number.");
        }
    }

    private static void viewTasks() {
        if (tasks.isEmpty()) {
            System.out.println("No tasks to display.");
        } else {
            for (int i = 0; i < tasks.size(); i++) {
                System.out.println((i + 1) + ". " + tasks.get(i));
            }
        }
    }
}


