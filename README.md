# expense_tracker.py

import json
from datetime import datetime

# File to store expenses
DATA_FILE = "expenses.json"

# Load existing expenses from file
def load_expenses():
    try:
        with open(DATA_FILE, "r") as f:
            return json.load(f)
    except FileNotFoundError:
        return []

# Save expenses to file
def save_expenses(expenses):
    with open(DATA_FILE, "w") as f:
        json.dump(expenses, f, indent=4)

def add_expense(expenses):
    amount = float(input("Enter amount: "))
    category = input("Enter category (food, travel, etc.): ")
    note = input("Enter note: ")
    date = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    
    expense = {
        "amount": amount,
        "category": category,
        "note": note,
        "date": date
    }
    expenses.append(expense)
    save_expenses(expenses)
    print("Expense added successfully!\n")

def view_expenses(expenses):
    if not expenses:
        print("No expenses recorded.\n")
        return
    for i, exp in enumerate(expenses, start=1):
        print(f"{i}. {exp['date']} - {exp['category']} - ₹{exp['amount']} ({exp['note']})")
    print()

def main():
    expenses = load_expenses()
    while True:
        print("=== Personal Expense Tracker ===")
        print("1. Add Expense")
        print("2. View Expenses")
        print("3. Exit")
        choice = input("Choose an option: ")

        if choice == "1":
            add_expense(expenses)
        elif choice == "2":
            view_expenses(expenses)
        elif choice == "3":
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Try again.\n")

if __name__ == "__main__":
    main()
