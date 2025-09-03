# HILL CIPHER
HILL CIPHER
## EX. NO: 3 IMPLEMENTATION OF HILL CIPHER
## AIM:
 To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B = 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is multiplied by an invertible n × n matrix, against modulus 26. To decrypt the message, each block is multiplied by the inverse of the matrix used for encryption. The matrix used for encryption is the cipher key, and it should be chosen

randomly from the set of invertible n × n matrices (modulo 26).
 
## ALGORITHM:

STEP-1: Read the plain text and key from the user.
STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM 
~~~
#include <stdio.h>
#include <string.h>
#include <ctype.h>
// Hill cipher key matrix and its inverse
int keymat[3][3] = { { 1, 2, 1 }, { 2, 3, 2 }, { 2, 2, 1 } };
int invkeymat[3][3] = { { -1, 0, 1 }, { 2, -1, 0 }, { -2, 2, -1 } };
// Key array for mapping
char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
// Encode function
void encode(char a, char b, char c, char *ret) {
    int x, y, z;
    int posa = (int) a - 65;
    int posb = (int) b - 65;
    int posc = (int) c - 65;
    x = posa * keymat[0][0] + posb * keymat[1][0] + posc * keymat[2][0];
    y = posa * keymat[0][1] + posb * keymat[1][1] + posc * keymat[2][1];
    z = posa * keymat[0][2] + posb * keymat[1][2] + posc * keymat[2][2];
    ret[0] = key[x % 26];
    ret[1] = key[y % 26];
    ret[2] = key[z % 26];
    ret[3] = '\0';
}
// Decode function
void decode(char a, char b, char c, char *ret) {
    int x, y, z;
    int posa = (int) a - 65;
    int posb = (int) b - 65;
    int posc = (int) c - 65;
    x = posa * invkeymat[0][0] + posb * invkeymat[1][0] + posc * invkeymat[2][0];
    y = posa * invkeymat[0][1] + posb * invkeymat[1][1] + posc * invkeymat[2][1];
    z = posa * invkeymat[0][2] + posb * invkeymat[1][2] + posc * invkeymat[2][2];
    ret[0] = key[(x % 26 < 0) ? (26 + x % 26) : (x % 26)];
    ret[1] = key[(y % 26 < 0) ? (26 + y % 26) : (y % 26)];
    ret[2] = key[(z % 26 < 0) ? (26 + z % 26) : (z % 26)];
    ret[3] = '\0';
}
int main() {
    char msg[1000];
    char enc[1000] = "";
    char dec[1000] = "";
    int n;
    printf("Simulation of Hill Cipher\n");
    printf("Input message : ");
    scanf("%s", msg);
    // Convert message to uppercase
    for (int i = 0; i < strlen(msg); i++) {
        msg[i] = toupper(msg[i]);
    }
    // Remove spaces (if needed)
    n = strlen(msg) % 3;
    // Append padding text 'X' if needed
    if (n != 0) {
        for (int i = 1; i <= (3 - n); i++) {
            strcat(msg, "X");
        }
    }
    printf("Padded message : %s\n", msg);
    // Encoding
    for (int i = 0; i < strlen(msg); i += 3) {
        char a = msg[i];
        char b = msg[i + 1];
        char c = msg[i + 2];
        char ret[4];
        encode(a, b, c, ret);
        strcat(enc, ret);
    }
    printf("Encoded message : %s\n", enc);
    // Decoding
    for (int i = 0; i < strlen(enc); i += 3) {
        char a = enc[i];
        char b = enc[i + 1];
        char c = enc[i + 2];
        char ret[4];
        decode(a, b, c, ret);
        strcat(dec, ret);
    }
    printf("Decoded message : %s\n", dec);
    return 0;
}
~~~

## OUTPUT

<img width="1908" height="933" alt="image" src="https://github.com/user-attachments/assets/1c4890b7-4518-4c09-a9f7-ea6e7333dba8" />


## RESULT
Successfully wrote a C program implementing the hill cipher substitution techniques.
