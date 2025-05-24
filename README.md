# Ex-4 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

void encrypt(char str[], int rails);
void decrypt(char str[], int rails);

int main() {
    int choice, rails;
    char str[1000];

    printf("Enter a Message: ");
    fgets(str, sizeof(str), stdin);  
    str[strcspn(str, "\n")] = '\0'; 

    printf("Enter number of rails: ");
    scanf("%d", &rails);

    printf("Choose an option:\n1. Encrypt\n2. Decrypt\n");
    scanf("%d", &choice);

    if (choice == 1) {
        encrypt(str, rails);
    } else if (choice == 2) {
        decrypt(str, rails);
    } else {
        printf("Invalid choice.\n");
    }

    return 0;
}

void encrypt(char str[], int rails) {
    int i, j, len, count;
    int code[100][1000]; 

    len = strlen(str);

    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            code[i][j] = 0;
        }
    }

    count = 0;  
    j = 0;      

    while (j < len) {
        if (count % 2 == 0) {
            for (i = 0; i < rails && j < len; i++) {
                code[i][j] = (int)str[j]; 
                j++;
            }
        } else {
            for (i = rails - 2; i > 0 && j < len; i--) {
                code[i][j] = (int)str[j]; 
                j++;
            }
        }
        count++;
    }

    printf("\nEncrypted Message: ");
    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            if (code[i][j] != 0) {
                printf("%c", code[i][j]);
            }
        }
    }
    printf("\n");
}

void decrypt(char str[], int rails) {
    int i, j, len, count;
    int code[100][1000];
    char decrypted[1000];

    len = strlen(str);

    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            code[i][j] = 0;
        }
    }

    count = 0;
    j = 0;
    int index = 0;

    while (j < len) {
        if (count % 2 == 0) {
            for (i = 0; i < rails && j < len; i++) {
                code[i][j] = 1; 
                j++;
            }
        } else {
            for (i = rails - 2; i > 0 && j < len; i--) {
                code[i][j] = 1; 
                j++;
            }
        }
        count++;
    }

    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            if (code[i][j] == 1) {
                code[i][j] = (int)str[index++];
            }
        }
    }

    index = 0;
    j = 0;

    while (j < len) {
        if (count % 2 == 0) {
            for (i = 0; i < rails && j < len; i++) {
                decrypted[j] = (char)code[i][j];
                j++;
            }
        } else {
            for (i = rails - 2; i > 0 && j < len; i--) {
                decrypted[j] = (char)code[i][j];
                j++;
            }
        }
        count++;
    }
    decrypted[j] = '\0';

    printf("\nDecrypted Message: %s\n", decrypted);
}

```

# OUTPUT


![Screenshot 2025-05-24 092219](https://github.com/user-attachments/assets/0b190ad6-d1a4-4a20-9d08-cf83e965438d)


# RESULT
thus the program executed.
