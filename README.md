# day-11
# Very Simple Employee Management System

def load_employees():
    employees = []
    try:
        with open("employee_data.txt", "r") as file:
            for line in file:
                name, dept, salary, year = line.strip().split(",")
                employees.append([name, dept, float(salary), int(year)])
    except FileNotFoundError:
        pass
    return employees

def save_employees(employees):
    with open("employee_data.txt", "w") as file:
        for emp in employees:
            file.write(f"{emp[0]},{emp[1]},{emp[2]},{emp[3]}\n")

def add_employee(employees):
    name = input("Enter name: ")
    dept = input("Enter department: ")
    try:
        salary = float(input("Enter salary: "))
        year = int(input("Enter joining year: "))
        employees.append([name, dept, salary, year])
        print("Employee added.\n")
    except ValueError:
        print("Invalid input. Please try again.\n")

def list_employees(employees):
    print("\nAll Employees:")
    for emp in employees:
        print(f"{emp[0]} | {emp[1]} | ${emp[2]} | Joined: {emp[3]}")
    print()

def search_employee(employees):
    term = input("Search by name or department: ").lower()
    print("\nSearch Results:")
    found = False
    for emp in employees:
        if term in emp[0].lower() or term in emp[1].lower():
            print(f"{emp[0]} | {emp[1]} | ${emp[2]} | Joined: {emp[3]}")
            found = True
    if not found:
        print("No match found.")
    print()

def sort_employees(employees):
    employees.sort(key=lambda e: e[2])
    print("Employees sorted by salary (low to high).\n")

def generate_report(employees):
    with open("employee_report.txt", "w") as file:
        file.write("Employee Report\n===============\n")
        for emp in employees:
            file.write(f"{emp[0]} | {emp[1]} | ${emp[2]} | Joined: {emp[3]}\n")
    print("Report generated.\n")

def show_menu():
    print("""
1. Add Employee
2. List Employees
3. Search Employee
4. Sort by Salary
5. Generate Report
6. Exit
""")

def main_program():
    employees = load_employees()
    while True:
        show_menu()
        choice = input("Choose an option (1-6): ")
        if choice == "1":
            add_employee(employees)
        elif choice == "2":
            list_employees(employees)
        elif choice == "3":
            search_employee(employees)
        elif choice == "4":
            sort_employees(employees)
        elif choice == "5":
            generate_report(employees)
        elif choice == "6":
            save_employees(employees)
            print("Goodbye!")
            break
        else:
            print("Invalid choice.\n")

# Start the program
main_program()
