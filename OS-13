#include <stdio.h>
#include <stdlib.h>
#define MEMORY_SIZE 1000
typedef struct Node {
    int start;
    int end;
    struct Node* next;
} Node;
Node* head = NULL;
void initializeMemory() {
    head = (Node*)malloc(sizeof(Node));
    head->start = 0;
    head->end = MEMORY_SIZE - 1;
    head->next = NULL;
}
void printMemory() {
    Node* temp = head;
    printf("Memory Blocks:\n");
    while (temp != NULL) {
        printf("[%d - %d]\n", temp->start, temp->end);
        temp = temp->next;
    }
    printf("\n");
}
void firstFit(int size) {
    Node* prev = NULL;
    Node* curr = head;

    while (curr != NULL) {
        if (curr->end - curr->start + 1 >= size) {
            printf("Memory allocated from %d to %d\n", curr->start, curr->start + size - 1);
            curr->start += size;
            if (curr->start > curr->end) {
                if (prev == NULL) {
                    head = head->next;
                } else {
                    prev->next = curr->next;
                }
                free(curr);
            }
            return;
        }
        prev = curr;
        curr = curr->next;
    }

    printf("Memory allocation failed: Not enough free memory\n");
}
void bestFit(int size) {
    Node* bestFitBlock = NULL;
    int minFragmentation = MEMORY_SIZE + 1;

    Node* prev = NULL;
    Node* curr = head;

    while (curr != NULL) {
        int fragmentation = curr->end - curr->start + 1 - size;
        if (fragmentation >= 0 && fragmentation < minFragmentation) {
            minFragmentation = fragmentation;
            bestFitBlock = curr;
        }
        curr = curr->next;
    }

    if (bestFitBlock != NULL) {
        printf("Memory allocated from %d to %d\n", bestFitBlock->start, bestFitBlock->start + size - 1);
        bestFitBlock->start += size;
        if (bestFitBlock->start > bestFitBlock->end) {
            if (prev == NULL) {
                head = head->next;
            } else {
                prev->next = bestFitBlock->next;
            }
            free(bestFitBlock);
        }
    } else {
        printf("Memory allocation failed: Not enough free memory\n");
    }
}
void worstFit(int size) {
    Node* worstFitBlock = NULL;
    int maxFragmentation = -1;
    Node* prev = NULL;
    Node* curr = head;

    while (curr != NULL) {
        int fragmentation = curr->end - curr->start + 1 - size;
        if (fragmentation >= 0 && fragmentation > maxFragmentation) {
            maxFragmentation = fragmentation;
            worstFitBlock = curr;
        }
        curr = curr->next;
    }

    if (worstFitBlock != NULL) {
        printf("Memory allocated from %d to %d\n", worstFitBlock->start, worstFitBlock->start + size - 1);
        worstFitBlock->start += size;
        if (worstFitBlock->start > worstFitBlock->end) {
            if (prev == NULL) {
                head = head->next;
            } else {
                prev->next = worstFitBlock->next;
            }
            free(worstFitBlock);
        }
    } else {
        printf("Memory allocation failed: Not enough free memory\n");
    }
}
void deallocate(int start, int size) {
    Node* prev = NULL;
    Node* curr = head;
    while (curr != NULL) {
        if (start == curr->end + 1) {
            curr->end += size;
            if (curr->next != NULL && curr->end + 1 == curr->next->start) {
                curr->end = curr->next->end;
                Node* temp = curr->next;
                curr->next = curr->next->next;
                free(temp);
            }
            return;
        } else if (start + size == curr->start) {
            curr->start -= size;
            if (prev != NULL && prev->end + 1 == curr->start) {
                prev->end = curr->end;
                prev->next = curr->next;
                free(curr);
            }
            return;
        }
        prev = curr;
        curr = curr->next;
    }
    printf("Memory deallocation failed: Invalid memory block\n");
}
int main() {
    initializeMemory();
    printMemory();
    printf("First Fit Allocation:\n");
    firstFit(200);
    firstFit(300);
    printMemory();
    printf("Memory Deallocation:\n");
    deallocate(200, 200);
    printMemory();
    printf("Best Fit Allocation:\n");
    bestFit(150);
    bestFit(250);
    printMemory();
    printf("Memory Deallocation:\n");
    deallocate(250, 250);
    printMemory();
    printf("Worst Fit Allocation:\n");
    worstFit(100);
    worstFit(400);
    printMemory();

    return 0;
}
