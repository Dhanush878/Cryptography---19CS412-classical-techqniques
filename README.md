# Cryptography---19CS412-classical-techqniques
# PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To implement a program to encrypt a plain text and decrypt a cipher text using play fair Cipher substitution technique.

 
## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

ALGORITHM DESCRIPTION:
The Playfair cipher uses a 5 by 5 table containing a key word or phrase. To generate the key table, first fill the spaces in the table with the letters of the keyword, then fill the remaining spaces with the rest of the letters of the alphabet in order (usually omitting "Q" to reduce the alphabet to fit; other versions put both "I" and "J" in the same space). The key can be written in the top rows of the table, from left to right, or in some other pattern, such as a spiral beginning in the upper-left-hand corner and ending in the centre.
The keyword together with the conventions for filling in the 5 by 5 table constitutes the cipher key. To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. Then apply the following 4 rules, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter. Encrypt the new pair and continue. Some   
   variants of Playfair use "Q" instead of "X", but any letter, itself uncommon as a repeated pair, will do.
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively (wrapping 
   around to the left side of the row if a letter in the original pair was on the right side of the row).
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively (wrapping around 
   to the top side of the column if a letter in the original pair was on the bottom side of the column).
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of 
   corners of the rectangle defined by the original pair. The order is important – the first letter of the encrypted pair is the one that 
    lies on the same row as the first letter of the plaintext pair.
To decrypt, use the INVERSE (opposite) of the last 3 rules, and the 1st as-is (dropping any extra "X"s, or "Q"s that do not make sense in the final message when finished).


## PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main()
{
    char key[] = "Monarchy";
    char text[] = "instruments";
    char table[5][5];
    int used[26] = {0};
    int i, j, k = 0, r1, c1, r2, c2;
    char a, b;

    used['j' - 'a'] = 1;

    for (i = 0; key[i]; i++)
    {
        a = tolower(key[i]);
        if (a == 'j') a = 'i';

        if (!used[a - 'a'])
        {
            table[k / 5][k % 5] = a;
            used[a - 'a'] = 1;
            k++;
        }
    }

    for (i = 0; i < 26; i++)
    {
        if (!used[i])
        {
            table[k / 5][k % 5] = 'a' + i;
            k++;
        }
    }

    printf("Key text: %s\n", key);
    printf("Plain text: %s\n", text);
    printf("Cipher text: ");

    for (i = 0; text[i]; i += 2)
    {
        a = text[i];
        b = text[i + 1];

        for (j = 0; j < 25; j++)
        {
            if (table[j / 5][j % 5] == a)
                r1 = j / 5, c1 = j % 5;

            if (table[j / 5][j % 5] == b)
                r2 = j / 5, c2 = j % 5;
        }

        if (r1 == r2)
        {
            a = table[r1][(c1 + 1) % 5];
            b = table[r2][(c2 + 1) % 5];
        }
        else if (c1 == c2)
        {
            a = table[(r1 + 1) % 5][c1];
            b = table[(r2 + 1) % 5][c2];
        }
        else
        {
            a = table[r1][c2];
            b = table[r2][c1];
        }

        printf("%c%c", a, b);
    }

    printf("\n");
    return 0;
}
```

## OUTPUT:
Output:
<img width="1917" height="803" alt="image" src="https://github.com/user-attachments/assets/f9a637ec-7a97-4832-a1a2-e189248ae59b" />

Key text: Monarchy Plain text: instruments Cipher text: gatlmzclrqtx

## RESULT:
The program is executed successfully
