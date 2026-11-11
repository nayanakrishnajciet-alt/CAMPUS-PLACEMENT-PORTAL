"# CAMPUS-PLACEMENT-PORTAL" 
//# Student-placement--system- Build a system to get placement submissions for students using LinkedIn lists.

#include <stdio.h> #include <stdlib.h> #include <string.h>

// Node structure for placement submission typedef struct Submission { int studentID; char skills[50]; char languageknowDate[20]; char status[20]; // Submitted / Pending struct Submission *next; } Submission;

Submission *head = NULL;

// Function to create a new node Submission* createSubmission(int studentID, char title[], char date[], char status[]) { Submission newNode = (Submission)malloc(sizeof(Submission)); newNode->studentID = studentID; strcpy(newNode->assignmentTitle, title); strcpy(newNode->submissionDate, date); strcpy(newNode->status, status); newNode->next = NULL; return newNode; }

// Add new submission void addSubmission(int studentID, char title[], char date[], char status[]) { Submission *newNode = createSubmission(studentID, title, date, status); if (head == NULL) { head = newNode; } else { Submission *temp = head; while (temp->next != NULL) temp = temp->next; temp->next = newNode; } printf("Submission record added successfully!\n"); }

// Update status by student ID and assignment title void updateStatus(int studentID, char title[], char newStatus[]) { Submission *temp = head; int found = 0; while (temp != NULL) { if (temp->studentID == studentID && strcmp(temp->assignmentTitle, title) == 0) { strcpy(temp->status, newStatus); printf("Status updated successfully!\n"); found = 1; break; } temp = temp->next; } if (!found) printf("Record not found!\n"); }

// Search submissions by student ID void searchByStudent(int studentID) { Submission *temp = head; int found = 0; printf("\n--- Submissions for Student ID %d ---\n", studentID); while (temp != NULL) { if (temp->studentID == studentID) { printf("Assignment: %s, Date: %s, Status: %s\n", temp->assignmentTitle, temp->submissionDate, temp->status); found = 1; } temp = temp->next; } if (!found) printf("No submissions found for Student ID %d\n", studentID); }

// Display all submissions void displayAll() { Submission *temp = head; if (temp == NULL) { printf("No submissions available!\n"); return; } printf("\n--- All Submissions ---\n"); while (temp != NULL) { printf("Student ID: %d, Assignment: %s, Date: %s, Status: %s\n", temp->studentID, temp->assignmentTitle, temp->submissionDate, temp->status); temp = temp->next; } }

// Main menu int main() { int choice, studentID; char title[50], date[20], status[20];

while (1) {
    printf("\n--- Student placement Submission  ---\n");
    printf("1. Add skills Record\n");
    printf("2. Update Status\n");
    printf("3. Search Submissions by Student ID\n");
    printf("4. Display All Records\n");
    printf("0. Exit\n");
    printf("Enter choice: ");
    scanf("%d", &choice);
    getchar();

    switch (choice) {
        case 1:
            printf("Enter Student ID: ");
            scanf("%d", &studentID);
            getchar();
            printf("Enter Assignment Title: ");
            fgets(title, sizeof(title), stdin);
            title[strcspn(title, "\n")] = 0;
            printf("Enter Submission Date (DD/MM/YYYY): ");
            scanf("%s", date);
            printf("Enter Status (Submitted/Pending): ");
            scanf("%s", status);
            addSubmission(studentID, title, date, status);
            break;

        case 2:
            printf("Enter Student ID: ");
            scanf("%d", &studentID);
            getchar();
            printf("Enter Assignment Title: ");
            fgets(title, sizeof(title), stdin);
            title[strcspn(title, "\n")] = 0;
            printf("Enter New Status: ");
            scanf("%s", status);
            updateStatus(studentID, title, status);
            break;

        case 3:
            printf("Enter Student ID: ");
            scanf("%d", &studentID);
            searchByStudent(studentID);
            break;

        case 4:
            displayAll();
            break;

        case 0:
            printf("Exiting program.\n");
            return 0;

        default:
            printf("Invalid choice! Try again.\n");
    }
}
}
