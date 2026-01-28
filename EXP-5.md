```c
#include <stdio.h>
#include <ctype.h>
#include <string.h>

int isValidIdentifier(char *str) {
    if (!isalpha(str[0]) && str[0] != '_')
        return 0;
    for (int i = 1; str[i] != '\0'; i++) {
        if (!isalnum(str[i]) && str[i] != '_')
            return 0;
    }
    return 1;
}

void analyze(char *code) {
    int whitespace_count = 0, newline_count = 0;
    char buffer[100];
    int index = 0;
    
    while (*code) {
        if (*code == '\n') {
            newline_count++;
        }
        if (isspace(*code)) {
            whitespace_count++;
            code++;
            continue;
        }
        if (strncmp(code, "//", 2) == 0) {
            printf("Single-line Comment\n");
            return;
        }
        if (strncmp(code, "/*", 2) == 0) {
            printf("Multi-line Comment\n");
            return;
        }
        if (isalpha(*code) || *code == '_') {
            index = 0;
            while (isalnum(*code) || *code == '_') {
                buffer[index++] = *code;
                code++;
            }
            buffer[index] = '\0';
            if (isValidIdentifier(buffer)) {
                printf("Valid Identifier: %s\n", buffer);
            } else {
                printf("Invalid Identifier: %s\n", buffer);
            }

            continue;
        }
        if (isdigit(*code)) {
            printf("Constant: %c\n", *code);
        } else if (*code == '+' || *code == '-' || *code == '*' || *code == '/') {
            printf("Operator: %c\n", *code);
        } else {
            printf("Symbol: %c\n", *code);
        }
        code++;
    }
    printf("Whitespace Count: %d\n", whitespace_count);
    printf("Newline Count: %d\n", newline_count);
}

int main() {
    char code1[] = "// This is a comment\n";
    char code2[] = "/* This is a multi-line comment */\n";
    char code3[] = "int x1 = 10 + 5 - 2 * 3 / 1;\n invalid#id 123var";
    
    analyze(code1);
    analyze(code2);
    analyze(code3);
    
    return 0;
}



```
<img width="571" height="242" alt="count frequency" src="https://github.com/user-attachments/assets/9e2c2284-30fb-411f-87a0-eda4db0005d0" />
