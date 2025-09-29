def show_menu():
    print("\n===== Expense Tracker Menu ======")
    print("1. Add Expense")
    print("2. View Expense")
    print("3. view Total Expense")
    print("4. Exit")


def add_expense():
    date = input("Enter date (yyyy-mm-dd):")
    category = input("Enter category (e.g., food, travel ....)")
    amount = input("Enter amount: ")

    with open("expenses.csv", "a") as file:
        file.write(f"{date},{category},{amount}\n")

    print("✅ Expense added successfully.")

def view_expenses():
    print("\n--- Your Expenses ---")
    try:
        with open("expenses.csv", "r") as file:
            for line in file:
                print(line.strip())
    except FileNotFoundError:
        print("No expenses found.")


def view_total():
    total = 0
    try:
        with open("expenses.csv", "r") as file:
            for line in file:
                parts = line.strip().split(",")
                if len(parts) == 3:
                    total += float(parts[2])
        print(f"\n Total spent: ₹{total}")
    except FileNotFoundError:
        print("No expenses found.")


while True:
    show_menu()
    choice = input("Choose an option (1-4): ")

    if choice == "1":
        add_expense()
    elif choice == "2":
        view_expenses()
    elif choice == "3":
        view_total()
    elif choice == "4":
        print("Goodbye!")
        break
    else:
        print("❌ Invalid choice. Please try again.")
