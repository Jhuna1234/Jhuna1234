#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define MAX_EMAIL_LENGTH 500
#define NUM_SPAM_KEYWORDS 10


const char *spamKeywords[NUM_SPAM_KEYWORDS] = {
    "free", "win", "winner", "click here", "buy now", "urgent", 
    "limited time", "lottery", "money", "offer"
};

// Convert string to lowercase
void toLowerCase(char *str) {
    for (int i = 0; str[i]; i++) {
        str[i] = tolower((unsigned char) str[i]);
    }
}
int isSpam(const char *email) {
    char lowerEmail[MAX_EMAIL_LENGTH];
    strncpy(lowerEmail, email, MAX_EMAIL_LENGTH);
    lowerEmail[MAX_EMAIL_LENGTH - 1] = '\0';
    toLowerCase(lowerEmail);
    
    for (int i = 0; i < NUM_SPAM_KEYWORDS; i++) {
        if (strstr(lowerEmail, spamKeywords[i]) != NULL) {
            return 1; // Email is spam
        }
    }
    return 0; // Email is not spam
}

int main() {
    char email[MAX_EMAIL_LENGTH];
    
    printf("Email Spam Filter\n");
    printf("Spam Keywords:\n");
    for (int i = 0; i < NUM_SPAM_KEYWORDS; i++) {
        printf("- %s\n", spamKeywords[i]);
    }

    while (1) {
        printf("\nEnter an email (or type 'exit' to quit): ");
        fgets(email, MAX_EMAIL_LENGTH, stdin);
        email[strcspn(email, "\n")] = 0; // Remove newline character

        if (strcmp(email, "exit") == 0) {
            break;
        }

        if (isSpam(email)) {
            printf("The email is classified as: SPAM\n");
        } else {
            printf("The email is classified as: NOT SPAM\n");
        }
    }
    
    return 0;
}
