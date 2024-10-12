# phonebook-with-c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Define the maximum number of contacts and their name/phone length
#define MAX 100
#define NAME_LENGTH 50
#define PHONE_LENGTH 15

// Contact structure to hold name and phone number
struct Contact {
    char name[NAME_LENGTH];
    char phone[PHONE_LENGTH];
};

// Phonebook array to hold contacts and count of contacts
struct Contact phonebook[MAX];
int contact_count = 0;

// Function to add a new contact
void add_contact() {
    if (contact_count < MAX) {
        printf("Enter Name: ");
        scanf(" %[^\n]s", phonebook[contact_count].name);
        printf("Enter Phone Number: ");
        scanf(" %[^\n]s", phonebook[contact_count].phone);
        contact_count++;
        printf("Contact added successfully!\n");
    } else {
        printf("Phonebook is full!\n");
    }
}

// Function to display all contacts
void display_contacts() {
    if (contact_count == 0) {
        printf("No contacts in the phonebook.\n");
    } else {
        printf("\n--- Phonebook Contacts ---\n");
        for (int i = 0; i < contact_count; i++) {
            printf("%d. Name: %s, Phone: %s\n", i + 1, phonebook[i].name, phonebook[i].phone);
        }
    }
}

// Function to search for a contact by name
void search_contact() {
    char search_name[NAME_LENGTH];
    printf("Enter name to search: ");
    scanf(" %[^\n]s", search_name);
    
    int found = 0;
    for (int i = 0; i < contact_count; i++) {
        if (strcmp(phonebook[i].name, search_name) == 0) {
            printf("Contact found: Name: %s, Phone: %s\n", phonebook[i].name, phonebook[i].phone);
            found = 1;
            break;
        }
    }
    if (!found) {
        printf("Contact not found!\n");
    }
}

// Function to delete a contact by name
void delete_contact() {
    char delete_name[NAME_LENGTH];
    printf("Enter name to delete: ");
    scanf(" %[^\n]s", delete_name);
    
    int found = 0;
    for (int i = 0; i < contact_count; i++) {
        if (strcmp(phonebook[i].name, delete_name) == 0) {
            found = 1;
            // Shift contacts to the left to overwrite the deleted contact
            for (int j = i; j < contact_count - 1; j++) {
                phonebook[j] = phonebook[j + 1];
            }
            contact_count--;
            printf("Contact deleted successfully!\n");
            break;
        }
    }
    if (!found) {
        printf("Contact not found!\n");
    }
}

// Function to display the menu
void menu() {
    printf("\n--- Phonebook Menu ---\n");
    printf("1. Add Contact\n");
    printf("2. Display Contacts\n");
    printf("3. Search Contact\n");
    printf("4. Delete Contact\n");
    printf("5. Exit\n");
}

int main() {
    int choice;
    
    do {
        menu();
        printf("Enter your choice: ");
        scanf("%d", &choice);
        
        switch (choice) {
            case 1:
                add_contact();
                break;
            case 2:
                display_contacts();
                break;
            case 3:
                search_contact();
                break;
            case 4:
                delete_contact();
                break;
            case 5:
                printf("Exiting Phonebook...\n");
                break;
            default:
                printf("Invalid choice! Please try again.\n");
        }
    } while (choice != 5);
    
    return 0;
}
