//link-list-at_beginning-
#include <stdio.h>
#include <stdlib.h>

// Define the structure for a node in the linked list
struct Node {
    int data;
    struct Node* next;
};

// Function to insert a new node at the beginning of the list
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

// Function to traverse and print the linked list
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

    // Prompt user for the number of nodes
    printf("Enter the number of nodes: ");
    scanf("%d", &n);

    if (n <= 0) {
        printf("Invalid number of nodes. Exiting...\n");
        return 1;
    }

    // Create the first node
    head = (struct Node*)malloc(sizeof(struct Node));
    if (head == NULL) {
        printf("Memory allocation failed. Exiting...\n");
        return 1;
    }

    printf("Enter data for node 1: ");
    scanf("%d", &head->data);
    head->next = NULL;
    temp = head;

    // Create the remaining nodes
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

    // Display the original linked list
    printf("\nOriginal linked list:\n");
    linklistTraversal(head);

    // Insert a new node at the beginning
    int newValue;
    printf("\nEnter a value to insert at the beginning: ");
    scanf("%d", &newValue);
    at_beginning(&head, newValue);

    // Display the linked list after insertion
    printf("\nLinked list after insertion:\n");
    linklistTraversal(head);

    // Free the allocated memory
    temp = head;
    while (temp != NULL) {
        struct Node* nextNode = temp->next;
        free(temp);
        temp = nextNode;
    }

    return 0;
}
