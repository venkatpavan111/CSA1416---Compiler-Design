```c
#include <stdio.h>
#include <ctype.h>
#include <string.h>

void analyze(char *code) {
    int whitespace_count = 0, newline_count = 0;
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
            printf("Identifier: %c\n", *code);
        } else if (isdigit(*code)) {
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
    char code3[] = "int x = 10 + 5 - 2 * 3 / 1;\n";
    
    analyze(code1);
    analyze(code2);
    analyze(code3);
    
    return 0;
}
```<img width="568" height="287" alt="relational operation" src="https://github.com/user-attachments/assets/e45910c5-195e-4f54-a594-ead15feb05fe" />


