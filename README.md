# experiment-6
exp6
#Create a Student Record Management System using linked list
• Use a singly/doubly linked list to store student data (Roll No, Name, Marks).
• Perform operations: Add, Delete, Update, Search, and Sort.
• Display records in ascending/descending order based on marks or roll number.


class Node:
    def __init__(self, roll_no, name, marks):
        self.roll_no = roll_no
        self.name = name
        self.marks = marks
        self.prev = None
        self.next = None


class StudentRecordManagement:
    def __init__(self):
        self.head = None

    def add_student(self, roll_no, name, marks):
        new_node = Node(roll_no, name, marks)
        if self.head is None:
            self.head = new_node
        else:
            temp = self.head
            while temp.next:
                temp = temp.next
            temp.next = new_node
            new_node.prev = temp
        print("✅ Student added successfully!")

    def delete_student(self, roll_no):
        temp = self.head
        while temp:
            if temp.roll_no == roll_no:
                if temp.prev:
                    temp.prev.next = temp.next
                if temp.next:
                    temp.next.prev = temp.prev
                if temp == self.head:
                    self.head = temp.next
                print("🗑️ Student deleted successfully!")
                return
            temp = temp.next
        print("❌ Student not found!")

    def update_student(self, roll_no, new_name, new_marks):
        temp = self.head
        while temp:
            if temp.roll_no == roll_no:
                temp.name = new_name
                temp.marks = new_marks
                print("✏️ Student updated successfully!")
                return
            temp = temp.next
        print("❌ Student not found!")

    def search_student(self, roll_no):
        temp = self.head
        while temp:
            if temp.roll_no == roll_no:
                print(f"🔍 Found -> Roll No: {temp.roll_no}, Name: {temp.name}, Marks: {temp.marks}")
                return
            temp = temp.next
        print("❌ Student not found!")

    def display_students(self, order_by="roll", ascending=True):
        students = []
        temp = self.head
        while temp:
            students.append((temp.roll_no, temp.name, temp.marks))
            temp = temp.next

        if order_by == "roll":
            students.sort(key=lambda x: x[0], reverse=not ascending)
        elif order_by == "marks":
            students.sort(key=lambda x: x[2], reverse=not ascending)

        print("\n📋 Student Records:")
        for s in students:
            print(f"Roll No: {s[0]}, Name: {s[1]}, Marks: {s[2]}")
        print()

    def sort_students(self, order_by="roll", ascending=True):
        # This is just a wrapper for display (sorting is done there)
        self.display_students(order_by, ascending)


# ------------------ MAIN MENU ------------------
def main():
    system = StudentRecordManagement()

    while True:
        print("\n====== Student Record Management System ======")
        print("1. Add Student")
        print("2. Delete Student")
        print("3. Update Student")
        print("4. Search Student")
        print("5. Display Students (by Roll No)")
        print("6. Display Students (by Marks)")
        print("7. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            roll = int(input("Enter Roll No: "))
            name = input("Enter Name: ")
            marks = float(input("Enter Marks: "))
            system.add_student(roll, name, marks)

        elif choice == "2":
            roll = int(input("Enter Roll No to Delete: "))
            system.delete_student(roll)

        elif choice == "3":
            roll = int(input("Enter Roll No to Update: "))
            name = input("Enter New Name: ")
            marks = float(input("Enter New Marks: "))
            system.update_student(roll, name, marks)

        elif choice == "4":
            roll = int(input("Enter Roll No to Search: "))
            system.search_student(roll)

        elif choice == "5":
            order = input("Sort by Roll No Ascending? (y/n): ")
            system.display_students(order_by="roll", ascending=(order.lower() == "y"))

        elif choice == "6":
            order = input("Sort by Marks Ascending? (y/n): ")
            system.display_students(order_by="marks", ascending=(order.lower() == "y"))

        elif choice == "7":
            print("👋 Exiting... Thank you!")
            break

        else:
            print("❌ Invalid choice! Try again.")


if __name__ == "__main__":
    main()
