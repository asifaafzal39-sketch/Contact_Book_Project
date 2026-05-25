# Contact_Book_Project

# File to store contacts
file_name = "contacts.txt"

# Function to add a new contact
def add_contact():
    name = input("Enter name: ")
    phone = input("Enter phone number: ")

    file = open(file_name, "a")  # append mode
    file.write(name + "," + phone + "\n")
    file.close()

    print("Contact added successfully!")

# Function to view all contacts
def view_contacts():
    try:
        file = open(file_name, "r")
        contacts = file.readlines()
        file.close()

        if len(contacts) == 0:
            print("No contacts found.")
        else:
            print("\nContact List:")
            for i in range(len(contacts)):
                name, phone = contacts[i].strip().split(",")
                print(i + 1, "- Name:", name, "| Phone:", phone)
    except:
        print("No contacts file found.")

# Function to search for a contact
def search_contact():
    search_name = input("Enter name to search: ")

    try:
        file = open(file_name, "r")
        contacts = file.readlines()
        file.close()

        found = False

        for contact in contacts:
            name, phone = contact.strip().split(",")
            if search_name.lower() == name.lower():
                print("Contact found!")
                print("Name:", name)
                print("Phone:", phone)
                found = True
                break

        if not found:
            print("Contact not found.")

    except:
        print("No contacts available.")

# Function to delete a contact
def delete_contact():
    try:
        file = open(file_name, "r")
        contacts = file.readlines()
        file.close()

        view_contacts()
        name_to_delete = input("Enter name to delete: ")

        new_contacts = []
        found = False

        for contact in contacts:
            name, phone = contact.strip().split(",")
            if name.lower() != name_to_delete.lower():
                new_contacts.append(contact)
            else:
                found = True

        file = open(file_name, "w")
        file.writelines(new_contacts)
        file.close()

        if found:
            print("Contact deleted successfully!")
        else:
            print("Contact not found.")

    except:
        print("No contacts available.")

# Main menu
while True:
    print("\n--- CONTACT BOOK MENU ---")
    print("1. Add Contact")
    print("2. View Contacts")
    print("3. Search Contact")
    print("4. Delete Contact")
    print("5. Exit")

    choice = input("Enter your choice: ")

    if choice == "1":
        add_contact()
    elif choice == "2":
        view_contacts()
    elif choice == "3":
        search_contact()
    elif choice == "4":
        delete_contact()
    elif choice == "5":
        print("Goodbye!")
        break
    else:
        print("Invalid choice. Try again.")
