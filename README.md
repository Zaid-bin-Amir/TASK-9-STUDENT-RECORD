# TASK-9-STUDENT-RECORD
# Student Record Program using Python lists

names = []
marks = []


def add_student():
    name = input("Enter student name: ").strip()
    try:
        mark = float(input("Enter marks (0-100): "))
    except ValueError:
        print("Invalid marks. Please enter a number.")
        return
    if not 0 <= mark <= 100:
        print("Marks must be between 0 and 100.")
        return
    names.append(name)
    marks.append(mark)
    print(f"Added {name} with {mark} marks.")


def display_all():
    if not names:
        print("No records yet.")
        return
    print(f"\n{'No.':<5}{'Name':<20}{'Marks':>8}")
    print("-" * 33)
    for i, (n, m) in enumerate(zip(names, marks), start=1):
        print(f"{i:<5}{n:<20}{m:>8.1f}")


def search_student():
    query = input("Enter name to search: ").strip().lower()
    found = False
    for n, m in zip(names, marks):
        if query in n.lower():
            print(f"Found: {n} -> {m}")
            found = True
    if not found:
        print("Student not found.")


def sort_records():
    if not names:
        print("No records to sort.")
        return
    choice = input("Sort by (1) Marks high-to-low, (2) Marks low-to-high, (3) Name A-Z: ")
    pairs = list(zip(names, marks))  # keeps names and marks synchronized

    if choice == "1":
        pairs.sort(key=lambda p: p[1], reverse=True)
    elif choice == "2":
        pairs.sort(key=lambda p: p[1])
    elif choice == "3":
        pairs.sort(key=lambda p: p[0].lower())
    else:
        print("Invalid choice.")
        return

    print(f"\n{'Name':<20}{'Marks':>8}")
    print("-" * 28)
    for n, m in pairs:
        print(f"{n:<20}{m:>8.1f}")


def highest_lowest():
    if not marks:
        print("No records yet.")
        return
    high, low = max(marks), min(marks)
    top = [names[i] for i, m in enumerate(marks) if m == high]
    bottom = [names[i] for i, m in enumerate(marks) if m == low]
    print(f"Highest score: {high} by {', '.join(top)}")
    print(f"Lowest score:  {low} by {', '.join(bottom)}")
    print(f"Average score: {sum(marks) / len(marks):.2f}")


def main():
    while True:
        print("\n=== Student Records ===")
        print("1. Add student")
        print("2. Display all")
        print("3. Search by name")
        print("4. Sort records")
        print("5. Highest / Lowest score")
        print("6. Exit")
        choice = input("Choose an option: ").strip()

        if choice == "1":
            add_student()
        elif choice == "2":
            display_all()
        elif choice == "3":
            search_student()
        elif choice == "4":
            sort_records()
        elif choice == "5":
            highest_lowest()
        elif choice == "6":
            print("Goodbye!")
            break
        else:
            print("Invalid option, try again.")


if __name__ == "__main__":
    main()
