# link-list-at_beginning-
#include <stdio.h>
#include <stdlib.h>


struct Node {
    int data;
    struct Node* next;
};

void at_beginning(struct Node** head, int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    if (newNode == NULL) {
        printf("Memory allocation failed\n");
        return;
    }
    newNode->data = value;
    newNode->next = *head;
    *head = newNode;
}
void linklistTraversal(struct Node* ptr) {
    while (ptr != NULL) {
        printf("%d -> ", ptr->data);
        ptr = ptr->next;
    }
    printf("NULL\n");
}

int main() {
    struct Node* head = NULL;
    struct Node* temp = NULL;
    struct Node* newNode = NULL;
    int n, data;


    printf("Enter the number of nodes: ");
    scanf("%d", &n);

    if (n <= 0) {
        printf("Invalid number of nodes. Exiting...\n");
        return 1;
    }


    head = (struct Node*)malloc(sizeof(struct Node));
    if (head == NULL) {
        printf("Memory allocation failed. Exiting...\n");
        return 1;
    }

    printf("Enter data for node 1: ");
    scanf("%d", &head->data);
    head->next = NULL;
    temp = head;

    for (int i = 2; i <= n; i++) {
        newNode = (struct Node*)malloc(sizeof(struct Node));
        if (newNode == NULL) {
            printf("Memory allocation failed. Exiting...\n");
            return 1;
        }

        printf("Enter data for node %d: ", i);
        scanf("%d", &newNode->data);
        newNode->next = NULL;

        temp->next = newNode;
        temp = newNode;
    }

    printf("\nOriginal linked list:\n");
    linklistTraversal(head);

    int newValue;
    printf("\nEnter a value to insert at the beginning: ");
    scanf("%d", &newValue);

    at_beginning(&head, newValue);


    printf("\nLinked list after insertion:\n");
    linklistTraversal(head);


    temp = head;
    while (temp != NULL) {
        struct Node* nextNode = temp->next;
        free(temp);
        temp = nextNode;
    }

    return 0;
}
