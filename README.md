# Ex.No: 1 E) IMPLEMENTATION OF RAIL FENCE CIPHER
### DATE: 27-02-2024                                                                          
### REGISTER NUMBER : 212221040021
### AIM: 
To implement the simple substitution technique named Rail Fence cipher using C language.
### Steps:
1. Read the Plain text.
2. Arrange the plain text in row columnar matrix format.
3. Now read the keyword depending on the number of columns of the plain text.
4. Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
5. Read the characters row wise or column wise in the former order to get the cipher text.



### Program:
```
#include <stdio.h>
#include <string.h>

void railFenceEncrypt(char *plaintext, int rails, char *ciphertext) {
    int len = strlen(plaintext);
    int i, j, k = 0;
    char railFence[rails][len];

    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            railFence[i][j] = '\0';
        }
    }

    int dir_down = 0;
    int row = 0;

    for (i = 0; i < len; i++) {
        if (row == 0 || row == rails - 1)
            dir_down = !dir_down;

        railFence[row][i] = plaintext[i];
        dir_down ? row++ : row--;
    }

    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            if (railFence[i][j] != '\0')
                ciphertext[k++] = railFence[i][j];
        }
    }
    ciphertext[k] = '\0';
}

void railFenceDecrypt(char *ciphertext, int rails, char *plaintext) {
    int len = strlen(ciphertext);
    int i, j, k = 0;
    char railFence[rails][len];

    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            railFence[i][j] = '\0';
        }
    }

    int dir_down = 0;
    int row = 0;

    for (i = 0; i < len; i++) {
        if (row == 0)
            dir_down = 1;
        if (row == rails - 1)
            dir_down = 0;

        railFence[row][i] = '*'; 

        dir_down ? row++ : row--;
    }

    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            if (railFence[i][j] == '*' && k < len) {
                railFence[i][j] = ciphertext[k++];
            }
        }
    }

    row = 0;
    dir_down = 0;

    for (i = 0; i < len; i++) {
        if (row == 0)
            dir_down = 1;
        if (row == rails - 1)
            dir_down = 0;

        if (railFence[row][i] != '*')
            plaintext[i] = railFence[row][i];

        dir_down ? row++ : row--;
    }
    plaintext[i] = '\0';
}

int main() {
    char text[100], ciphertext[100], decrypted[100];
    int choice, rails;

    printf("Choose an option:\n");
    printf("1. Encryption\n");
    printf("2. Decryption\n");
    printf("Enter your choice: ");
    scanf("%d", &choice);

    printf("Enter the text: ");
    getchar(); 
    fgets(text, sizeof(text), stdin);

    printf("Enter the number of rails: ");
    scanf("%d", &rails);

    switch(choice) {
        case 1:
            railFenceEncrypt(text, rails, ciphertext);
            printf("Encrypted Text: %s\n", ciphertext);
            break;
        case 2:
            railFenceDecrypt(text, rails, decrypted);
            printf("Decrypted Text: %s\n", decrypted);
            break;
        default:
            printf("Invalid choice.\n");
    }

    return 0;
}

```


### Output:

## Encryption:

## Decryption:


### Result:
Thus the implementation of Rail Fence cipher had been executed successfully.
