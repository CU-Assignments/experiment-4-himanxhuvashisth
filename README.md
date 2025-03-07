# expp-4


Chapter-4 (Collection Framework and MultiThreading) (Experiment 4)

	Use of Collections in Java. ArrayList, LinkedList, HashMap, TreeMap, HashSet in Java. Multithreading in Java. Thread Synchronization. Thread Priority, Thread LifeCycle.
	Develop Java programs using core concepts such as data structures, collections, and multithreading to manage and manipulate data.

Easy Level:
Write a Java program to implement an ArrayList that stores employee details (ID, Name, and Salary). Allow users to add, update, remove, and search employees.
		
  
Medium Level:
 Create a program to collect and store all the cards to assist the users in finding all the cards in a given symbol using Collection interface.

Hard Level:
Develop a ticket booking system with synchronized threads to ensure no double booking of seats. Use thread priorities to simulate VIP bookings being processed first.




###code###



import java.util.ArrayList;
import java.util.Scanner;

class Employee {
    int id;
    String name;
    double salary;

    Employee(int id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }

    public String toString() {
        return "ID: " + id + ", Name: " + name + ", Salary: $" + salary;
    }
}

public class EmployeeManager {
    static ArrayList<Employee> employees = new ArrayList<>();
    static Scanner scanner = new Scanner(System.in);

    public static void addEmployee() {
        System.out.print("Enter Employee ID: ");
        int id = scanner.nextInt();
        scanner.nextLine(); // Consume newline
        System.out.print("Enter Employee Name: ");
        String name = scanner.nextLine();
        System.out.print("Enter Employee Salary: ");
        double salary = scanner.nextDouble();
        employees.add(new Employee(id, name, salary));
        System.out.println("Employee added successfully!");
    }

    public static void updateEmployee() {
        System.out.print("Enter Employee ID to update: ");
        int id = scanner.nextInt();
        for (Employee emp : employees) {
            if (emp.id == id) {
                scanner.nextLine(); // Consume newline
                System.out.print("Enter New Name: ");
                emp.name = scanner.nextLine();
                System.out.print("Enter New Salary: ");
                emp.salary = scanner.nextDouble();
                System.out.println("Employee updated successfully!");
                return;
            }
        }
        System.out.println("Employee not found.");
    }

    public static void removeEmployee() {
        System.out.print("Enter Employee ID to remove: ");
        int id = scanner.nextInt();
        employees.removeIf(emp -> emp.id == id);
        System.out.println("Employee removed successfully!");
    }

    public static void searchEmployee() {
        System.out.print("Enter Employee ID to search: ");
        int id = scanner.nextInt();
        for (Employee emp : employees) {
            if (emp.id == id) {
                System.out.println(emp);
                return;
            }
        }
        System.out.println("Employee not found.");
    }

    public static void main(String[] args) {
        while (true) {
            System.out.println("\n1. Add Employee\n2. Update Employee\n3. Remove Employee\n4. Search Employee\n5. Exit");
            System.out.print("Enter choice: ");
            int choice = scanner.nextInt();
            switch (choice) {
                case 1: addEmployee(); break;
                case 2: updateEmployee(); break;
                case 3: removeEmployee(); break;
                case 4: searchEmployee(); break;
                case 5: System.exit(0);
                default: System.out.println("Invalid choice!");
            }
        }
    }
}



### MEDIUM CODE #####

import java.util.*;

class Card {
    String symbol;
    String value;

    Card(String symbol, String value) {
        this.symbol = symbol;
        this.value = value;
    }

    public String toString() {
        return value + " of " + symbol;
    }
}

public class CardCollection {
    static HashMap<String, ArrayList<Card>> cardMap = new HashMap<>();
    static Scanner scanner = new Scanner(System.in);

    public static void addCard() {
        System.out.print("Enter Card Symbol (e.g., Hearts, Spades): ");
        String symbol = scanner.next();
        System.out.print("Enter Card Value (e.g., Ace, King, 2): ");
        String value = scanner.next();

        cardMap.putIfAbsent(symbol, new ArrayList<>());
        cardMap.get(symbol).add(new Card(symbol, value));

        System.out.println("Card added successfully!");
    }

    public static void findCardsBySymbol() {
        System.out.print("Enter Symbol to search: ");
        String symbol = scanner.next();
        if (cardMap.containsKey(symbol)) {
            System.out.println("Cards in " + symbol + ": " + cardMap.get(symbol));
        } else {
            System.out.println("No cards found for this symbol.");
        }
    }

    public static void main(String[] args) {
        while (true) {
            System.out.println("\n1. Add Card\n2. Find Cards by Symbol\n3. Exit");
            System.out.print("Enter choice: ");
            int choice = scanner.nextInt();
            switch (choice) {
                case 1: addCard(); break;
                case 2: findCardsBySymbol(); break;
                case 3: System.exit(0);
                default: System.out.println("Invalid choice!");
            }
        }
    }
}
