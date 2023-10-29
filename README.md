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
==============







