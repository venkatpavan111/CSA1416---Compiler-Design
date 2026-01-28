```c
#include <stdio.h>
#include <stdbool.h>
#include <string.h>

bool is_valid_grammar(const char *str, int start, int end) {
    if (start > end) return true;
    if (str[start] == 'a' && str[end] == 'b') {
        return is_valid_grammar(str, start + 1, end - 1);
    }
    return false;
}

bool check_grammar(const char *str) {
    return is_valid_grammar(str, 0, strlen(str) - 1);
}

int main() {
    char input[100];

    printf("Enter a string: ");
    scanf("%s", input);

    if (check_grammar(input)) {
        printf("The string satisfies the grammar.\n");
    } else {
        printf("The string does not satisfy the grammar.\n");
    }

    return 0;
}
```
<img width="605" height="450" alt="mobile" src="https://github.com/user-attachments/assets/6a8ffc01-2e17-42f1-8adc-62a07b21c89a" />





