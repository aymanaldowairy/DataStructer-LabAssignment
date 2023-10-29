# DataStructer-LabAssignment

1- Write a function that adds all odd numbers to the beginning of the list and all even 
numbers to the end of the list until -1 is entered from the keyboard.

#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node* link;
};

void addFront(struct node** head, int data) {
    struct node* newNode = (struct node*)malloc(sizeof(struct node));
    newNode->data = data;
    newNode->link = *head;
    *head = newNode;
}

void addEnd(struct node* head, int data) {
    struct node* newNode = (struct node*)malloc(sizeof(struct node));
    newNode->data = data;
    newNode->link = NULL;

    while (head->link != NULL) {
        head = head->link;
    }
    head->link = newNode;
}

int main() {
    struct node* list = NULL;
    int num;

    printf("Enter numbers (-1 to stop):\n");

    while (1) {
        scanf("%d", &num);

        if (num == -1) {
            break;
        }

        if (num % 2 == 1) {  // Odd number
            addFront(&list, num);
        } else {  // Even number
            addEnd(list, num);
        }
    }

    printf("Resulting List:\n");

    struct node* current = list;
    while (current != NULL) {
        printf("%d ", current->data);
        current = current->link;
    }

    // Free dynamically allocated memory to avoid memory leaks
    while (list != NULL) {
        struct node* temp = list;
        list = list->link;
        free(temp);
    }

    return 0;
}
-----------------------------------------------------------------------------------------------
2- Add 100 randomly generated numbers to the list, write the c code that sorts all the 
numbers entered from largest to smallest and prints them on the screen.


#include <stdio.h>
#include <stdlib.h>
#include <time.h>

struct node {
    int data;
    struct node* link;
};

void addFront(struct node** head, int data) {
    struct node* newNode = (struct node*)malloc(sizeof(struct node));
    newNode->data = data;
    newNode->link = *head;
    *head = newNode;
}

void bubbleSort(struct node* head) {
    int swapped;
    struct node* ptr;
    struct node* lptr = NULL;

    if (head == NULL) {
        return; // Empty list
    }

    do {
        swapped = 0;
        ptr = head;

        while (ptr->link != lptr) {
            if (ptr->data < ptr->link->data) {
                // Swap the data values
                int temp = ptr->data;
                ptr->data = ptr->link->data;
                ptr->link->data = temp;
                swapped = 1;
            }
            ptr = ptr->link;
        }
        lptr = ptr;
    } while (swapped);
}

int main() {
    srand(time(NULL)); // Seed the random number generator

    struct node* list = NULL;

    // Add 100 random numbers to the list
    for (int i = 0; i < 100; i++) {
        int num = rand() % 1000; // Generate random numbers between 0 and 999
        addFront(&list, num);
    }

    printf("Original List:\n");

    struct node* current = list;
    while (current != NULL) {
        printf("%d ", current->data);
        current = current->link;
    }

    bubbleSort(list);

    printf("\nSorted List (Descending Order):\n");

    current = list;
    while (current != NULL) {
        printf("%d ", current->data);
        current = current->link;
    }

    // Free dynamically allocated memory to avoid memory leaks
    while (list != NULL) {
        struct node* temp = list;
        list = list->link;
        free(temp);
    }

    return 0;
}
----------------------------------------------------------------------------------------------------------------
3- Output : 54->58->62->65->71->73->……102

#include <stdio.h>

int main() {
    int currentNumber = 54;
    int increment = 4;
    int numberOfTerms = 10; // You can change this to the number of terms you want to generate

    for (int i = 0; i < numberOfTerms; i++) {
        printf("%d", currentNumber);

        if (i < numberOfTerms - 1) {
            printf("->");
        }

        currentNumber += increment;
    }

    printf("\n");

    return 0;
}
------------------------------------------------------------------------------------------------------------------ 
4- Write a function that stores the student number, name and age, traverses all the nodes in 
the list, writes all the student information on the screen and counts it. 
The output should look like this on the screen: 
1- Saliha 27 201 
2- Ece 19 203

#include <stdio.h>
#include <stdlib.h>

struct Student {
    int studentNumber;
    char name[50];
    int age;
    struct Student* next;
};

void addStudent(struct Student** head, int studentNumber, const char* name, int age) {
    struct Student* newNode = (struct Student*)malloc(sizeof(struct Student));
    newNode->studentNumber = studentNumber;
    snprintf(newNode->name, sizeof(newNode->name), "%s", name); // Copy the name
    newNode->age = age;
    newNode->next = *head;
    *head = newNode;
}

void printStudents(struct Student* head) {
    int count = 1;
    while (head != NULL) {
        printf("%d- %s %d %d\n", count, head->name, head->age, head->studentNumber);
        count++;
        head = head->next;
    }
}

int main() {
    struct Student* studentList = NULL;

    // Add students to the list
    addStudent(&studentList, 201, "Saliha", 27);
    addStudent(&studentList, 203, "Ece", 19);

    // Print student information and count
    printStudents(studentList);

    // Free dynamically allocated memory to avoid memory leaks
    while (studentList != NULL) {
        struct Student* temp = studentList;
        studentList = studentList->next;
        free(temp);
    }

    return 0;
}
------------------------------------------------------------------------------------------
5- Write the function that searches records by student name in the list.

#include <stdio.h>
#include <string.h>

// Define a structure to represent a student record
struct StudentRecord {
    char name[50];
    int rollNumber;
    // Add other fields as needed
};

// Function to search for a student by name in a list of records
int searchStudentByName(struct StudentRecord records[], int numRecords, const char* searchName) {
    for (int i = 0; i < numRecords; i++) {
        if (strcmp(records[i].name, searchName) == 0) {
            return i; // Return the index of the found record
        }
    }
    return -1; // Return -1 if the name is not found
}

int main() {
    // Example usage of the searchStudentByName function
    struct StudentRecord records[] = {
        {"ali", 101},
        {"osman", 102},
        {"okay", 103},
        // Add more records here
    };
    int numRecords = sizeof(records) / sizeof(records[0]);

    const char* searchName = "osman";
    int result = searchStudentByName(records, numRecords, searchName);

    if (result != -1) {
        printf("Student found at index %d\n", result);
        printf("Name: %s, Roll Number: %d\n", records[result].name, records[result].rollNumber);
    } else {
        printf("Student not found.\n");
    }

    return 0;
}
------------------------------------------------------------------------------------------------------------------------
6- Write the function that deletes the next node from the node with the searched student 
name in the list. 

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Define a structure to represent a student record
struct StudentRecord {
    char name[50];
    int rollNumber;
    // Add other fields as needed
};

// Define the structure for a node in the linked list
struct Node {
    struct StudentRecord data;
    struct Node* next;
};

// Function to delete the next node from the node with the specified student name
void deleteNextNode(struct Node* head, const char* searchName) {
    struct Node* current = head;
    while (current != NULL && current->next != NULL) {
        if (strcmp(current->data.name, searchName) == 0) {
            // Found the node with the specified name
            struct Node* temp = current->next;
            current->next = temp->next;
            free(temp); // Free the memory of the next node
            return;
        }
        current = current->next;
    }
}

// Function to print the linked list
void printLinkedList(struct Node* head) {
    struct Node* current = head;
    while (current != NULL) {
        printf("Name: %s, Roll Number: %d\n", current->data.name, current->data.rollNumber);
        current = current->next;
    }
}

int main() {
    // Example usage of the deleteNextNode function
    struct Node* head = NULL;
    // Create a linked list with some student records

    // Insert nodes (student records) into the linked list
    struct Node* newNode1 = (struct Node*)malloc(sizeof(struct Node));
    strcpy(newNode1->data.name, "Ali");
    newNode1->data.rollNumber = 101;
    newNode1->next = head;
    head = newNode1;

    struct Node* newNode2 = (struct Node*)malloc(sizeof(struct Node));
    strcpy(newNode2->data.name, "osman");
    newNode2->data.rollNumber = 102;
    newNode2->next = head;
    head = newNode2;

    struct Node* newNode3 = (struct Node*)malloc(sizeof(struct Node));
    strcpy(newNode3->data.name, "okay");
    newNode3->data.rollNumber = 103;
    newNode3->next = head;
    head = newNode3;

    // Print the original linked list
    printf("Original Linked List:\n");
    printLinkedList(head);

    // Delete the next node after "Bob" in the list
    deleteNextNode(head, "osman");

    // Print the modified linked list
    printf("\nLinked List after Deletion:\n");
    printLinkedList(head);

    // Free the memory for the linked list nodes
    while (head != NULL) {
        struct Node* temp = head;
        head = head->next;
        free(temp);
    }

    return 0;
}
------------------------------------------------------------------------------------
7- Write the function that prints the record with the longest name in the list. 
Output : the longest name in the list: Abdurrahmangazi 
Length : 15

#include <stdio.h>
#include <string.h>

// Define a structure to represent a student record
struct StudentRecord {
    char name[50];
    int rollNumber;
    // Add other fields as needed
};

// Function to find and print the record with the longest name in the list
void printRecordWithLongestName(struct StudentRecord records[], int numRecords) {
    int maxLength = 0;
    int longestNameIndex = -1;

    for (int i = 0; i < numRecords; i++) {
        int nameLength = strlen(records[i].name);
        if (nameLength > maxLength) {
            maxLength = nameLength;
            longestNameIndex = i;
        }
    }

    if (longestNameIndex != -1) {
        printf("The longest name in the list: %s\n", records[longestNameIndex].name);
        printf("Length: %d\n", maxLength);
    } else {
        printf("The list is empty.\n");
    }
}

int main() {
    // Example usage of the printRecordWithLongestName function
    struct StudentRecord records[] = {
        {"okay", 101},
        {"Ali", 102},
        {"Abdurrahmangazi", 103},
        {"osman", 104},
        // Add more records here
    };
    int numRecords = sizeof(records) / sizeof(records[0]);

    printRecordWithLongestName(records, numRecords);

    return 0;
}







