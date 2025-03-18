# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:

To develop a simple C program to implement Rail Fence Cipher.

## DESIGN STEPS:

### Step 1:

Design of Rail Fence Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
In the rail fence cipher, the plaintext is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

## PROGRAM:
```python
Developed By : SANJAY M
Register No  : 212223230187
```

```PYTHON
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

void encryptRailFence(char str[], int rails, char encrypted[]) {
    int i, j, len, count, code[100][1000];
    len = strlen(str);

    // Initialize the code array to 0
    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            code[i][j] = 0;
        }
    }

    count = 0;
    j = 0;
    while (j < len) {
        if (count % 2 == 0) { // Moving down the rails
            for (i = 0; i < rails && j < len; i++) {
                code[i][j] = (int)str[j];
                j++;
            }
        } else { // Moving up the rails
            for (i = rails - 2; i > 0 && j < len; i--) {
                code[i][j] = (int)str[j];
                j++;
            }
        }
        count++;
    }

    // Construct the encrypted message
    int pos = 0;
    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            if (code[i][j] != 0) {
                encrypted[pos++] = code[i][j];
            }
        }
    }
    encrypted[pos] = '\0'; // Null-terminate the string
}

void decryptRailFence(char str[], int rails, char decrypted[]) {
    int i, j, len, count, code[100][1000], pos = 0;
    len = strlen(str);

    // Initialize the code array to 0
    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            code[i][j] = 0;
        }
    }

    // Mark the positions where characters will go
    count = 0;
    j = 0;
    while (j < len) {
        if (count % 2 == 0) { // Moving down the rails
            for (i = 0; i < rails && j < len; i++) {
                code[i][j] = 1;
                j++;
            }
        } else { // Moving up the rails
            for (i = rails - 2; i > 0 && j < len; i--) {
                code[i][j] = 1;
                j++;
            }
        }
        count++;
    }

    // Fill the marked positions with the characters from the cipher text
    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            if (code[i][j] == 1) {
                code[i][j] = str[pos++];
            }
        }
    }

    // Reconstruct the decrypted message by following the zigzag pattern
    pos = 0;
    count = 0;
    j = 0;
    while (j < len) {
        if (count % 2 == 0) { // Moving down the rails
            for (i = 0; i < rails && j < len; i++) {
                if (code[i][j] != 0) {
                    decrypted[pos++] = code[i][j];
                }
                j++;
            }
        } else { // Moving up the rails
            for (i = rails - 2; i > 0 && j < len; i--) {
                if (code[i][j] != 0) {
                    decrypted[pos++] = code[i][j];
                }
                j++;
            }
        }
        count++;
    }
    decrypted[pos] = '\0'; // Null-terminate the string
}

int main() {
    char str[1000], encrypted[1000], decrypted[1000];
    int rails;
    printf("Simulating Rail Fence Cipher\n");

    printf("Enter a Secret Message: ");
    fgets(str, sizeof(str), stdin);
    str[strcspn(str, "\n")] = 0; // Remove trailing newline character if exists

    printf("Enter number of rails: ");
    scanf("%d", &rails);

    // Encrypt the message
    encryptRailFence(str, rails, encrypted);
    printf("Encrypted Message: %s\n", encrypted);

    // Decrypt the message
    decryptRailFence(encrypted, rails, decrypted);
    printf("Decrypted Message: %s\n", decrypted);

    return 0;
}
```
## OUTPUT:

![image](https://github.com/user-attachments/assets/49f4ac99-c5c3-4ad7-9a06-4023a150960a)
```
Enter a Secret Message: SANJAY
Enter number of rails: 4
Encrypted Message: SAYNAJ
Decrypted Message: SANJAY
```
## RESULT:
The program is executed successfully
