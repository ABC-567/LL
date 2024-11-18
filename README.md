# LL

// // DELETION OF NODE

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Node
{
    char name[50];
    int age;
    int RollNo;
    struct Node *next;
};

struct Node *createNode(char *name, int age, int RollNo)
{
    struct Node *newNode = (struct Node *)malloc(sizeof(struct Node));

    strcpy(newNode->name, name);
    newNode->age = age;
    newNode->RollNo = RollNo;
    newNode->next = NULL;
    return newNode;
}

void append(struct Node **head, char *name, int age, int RollNo)
{
    struct Node *newNode = createNode(name, age, RollNo);

    if (*head == NULL)
    {
        *head = newNode;
        return;
    }

    struct Node *last = *head;
    while (last->next != NULL)
    {
        last = last->next;
    }

    last->next = newNode;
}

void deleteNode(struct Node **head, int RollNo)
{
    struct Node *temp = *head;
    struct Node *prev = NULL;

    if (temp != NULL && temp->RollNo == RollNo)
    {
        *head = temp->next;
        free(temp);
        return;
    }

    while (temp != NULL && temp->RollNo != RollNo)
    {
        prev = temp;
        temp = temp->next;
    }

    if (temp == NULL)
    {
        printf("Student with roll number %d not found.\n", RollNo);
        return;
    }

    prev->next = temp->next;
    free(temp);
}

void display(struct Node *node)
{
    while (node != NULL)
    {
        printf("Name: %s, Age: %d, Roll No: %d\n", node->name, node->age, node->RollNo);
        node = node->next;
    }
}

int main()
{
    struct Node *head = NULL;

    append(&head, "Kinshunk", 16, 101);
    append(&head, "Paridhi", 17, 102);
    append(&head, "Aman", 16, 103);

    printf("Initial List:\n");
    display(head);

    deleteNode(&head, 102);

    printf("\nList after deleting student with roll number 102:\n");
    display(head);

    return 0;
}
