class Node:
    def __init__(self, data=None):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def insert(self, data):
        if not self.head:
            self.head = Node(data)
        else:
            current = self.head
            while current.next:
                current = current.next
            current.next = Node(data)

    def display(self):
        elements = []
        current_node = self.head
        while current_node:
            elements.append(current_node.data)
            current_node = current_node.next
        return elements

class Stack:
    def __init__(self):
        self.stack = []

    def push(self, item):
        self.stack.append(item)

    def pop(self):
        if not self.is_empty():
            return self.stack.pop()
        else:
            return None

    def is_empty(self):
        return len(self.stack) == 0

    def display(self):
        return self.stack

class Queue:
    def __init__(self):
        self.queue = []

    def enqueue(self, item):
        self.queue.append(item)

    def dequeue(self):
        if not self.is_empty():
            return self.queue.pop(0)
        else:
            return None

    def is_empty(self):
        return len(self.queue) == 0

    def display(self):
        return self.queue

# Library Management System
class Library:
    def __init__(self):
        self.books = []
        self.borrowed_books = Stack()
        self.borrowing_queue = Queue()
        self.members = LinkedList()

    def add_book(self):
        title = input("Enter book title: ")
        author = input("Enter book author: ")
        self.books.append({"title": title, "author": author})
        print("Book added successfully!")

    def display_books(self):
        print("Available books:")
        for i, book in enumerate(self.books):
            print(f"{i+1}. {book['title']} by {book['author']}")

    def borrow_book(self):
        self.display_books()
        book_choice = int(input("Enter the number of the book you want to borrow: ")) - 1
        if book_choice < 0 or book_choice >= len(self.books):
            print("Invalid book choice!")
        else:
            chosen_book = self.books[book_choice]
            self.borrowed_books.push(chosen_book)
            self.books.pop(book_choice)
            member_name = input("Enter your name: ")
            self.members.insert(member_name)
            self.borrowing_queue.enqueue(member_name)
            print(f"You have borrowed '{chosen_book['title']}' successfully!")

    def return_book(self):
        if self.borrowed_books.is_empty():
            print("No books are currently borrowed!")
        else:
            returned_book = self.borrowed_books.pop()
            self.books.append(returned_book)
            self.borrowing_queue.dequeue()
            print(f"You have returned '{returned_book['title']}' successfully!")

    def display_borrowed_books(self):
        print("Borrowed books:")
        for book in self.borrowed_books.display():
            print(f"{book['title']} by {book['author']}")

    def display_borrowing_queue(self):
        print("Borrowing queue:")
        for member in self.borrowing_queue.display():
            print(member)

    def display_members(self):
        print("Members:")
        for member in self.members.display():
            print(member)

def main():
    library = Library()

    while True:
        print("\nLibrary Management System")
        print("1. Add book")
        print("2. Display books")
        print("3. Borrow book")
        print("4. Return book")
        print("5. Display borrowed books")
        print("6. Display borrowing queue")
        print("7. Display members")
        print("8. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            library.add_book()
        elif choice == "2":
            library.display_books()
        elif choice == "3":
            library.borrow_book()
        elif choice == "4":
            library.return_book()
        elif choice == "5":
            library.display_borrowed_books()
        elif choice == "6":
            library.display_borrowing_queue()
        elif choice == "7":
            library.display_members()
        elif choice == "8":
            print("Exiting the system. Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()


