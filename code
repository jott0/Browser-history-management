#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>
#define MAX_HISTORY_SIZE 10
struct Webpage {
    char url[100];
    time_t timestamp;
    struct Webpage *prev;
    struct Webpage *next;
};
struct Webpage *history = NULL;
void addWebpage(char url[]) {
    struct Webpage *newPage = (struct Webpage *)malloc(sizeof(struct Webpage));
    strcpy(newPage->url, url);
    newPage->timestamp = time(NULL);
    newPage->prev = NULL;
    newPage->next = history;
    if (history != NULL) {
        history->prev = newPage;
    }
    history = newPage;
}
void displayHistory() {
    struct Webpage *current = history;
    while (current != NULL) {
        printf("URL: %s, Timestamp: %s", current->url, asctime(localtime(&(current->timestamp))));
        current = current->next;
    }
}
void clearHistory() {
    struct Webpage *current = history;
    while (current != NULL) {
        struct Webpage *temp = current;
        current = current->next;
        free(temp);
    }
    history = NULL;
}

void deleteWebpage(char url[]) {
    struct Webpage *current = history;
    while (current != NULL) {
        if (strcmp(current->url, url) == 0) {
            if (current->prev != NULL) {
                current->prev->next = current->next;
            } else {
                history = current->next;
            }
            if (current->next != NULL) {
                current->next->prev = current->prev;
            }
            free(current);
            return;
        }
        current = current->next;
    }
    printf("URL not found in history.\n");
}

int main() {
    char input[100];
    char deleteInput[100];
    int choice;
    while (1) {
        printf("\n1. Enter URL to add to history.\n");
        printf("2. Display browsing history.\n");
        printf("3. Enter URL to delete history.\n");
        printf("4. Clear history.\n");
        printf("5. Exit.\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        printf("\n");
        switch(choice){
            case 1:
                printf("Enter URL to add to browser history: ");
                scanf("%s", input);
                addWebpage(input);
                break;
            case 2:
                printf("Browsing History:\n");
                displayHistory();
                break;
            case 3:
                printf("Enter a URL to delete from history: ");
                scanf("%s", deleteInput);
                deleteWebpage(deleteInput);
                break;
            case 4:
                clearHistory();
                printf("History cleared.\n");
                break;
            case 5:
                exit(0);
            default:
                printf("Invalid choice. Please try again\n");
        }
    }
    return 0;
}
