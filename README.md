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




