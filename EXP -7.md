```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_RULES 10
#define MAX_LEN 100

typedef struct {
    char non_terminal;
    char *productions[MAX_RULES];
    int prod_count;
} Rule;

void eliminate_left_factoring(Rule *rules, int rule_count) {
    for (int i = 0; i < rule_count; i++) {
        char non_terminal = rules[i].non_terminal;
        char common_prefix[MAX_LEN] = {0};
        
        for (int j = 0; j < rules[i].prod_count - 1; j++) {
            for (int k = j + 1; k < rules[i].prod_count; k++) {
                int l = 0;
                while (rules[i].productions[j][l] != '\0' && rules[i].productions[j][l] == rules[i].productions[k][l]) {
                    common_prefix[l] = rules[i].productions[j][l];
                    l++;
                }
                common_prefix[l] = '\0';

                if (l > 0) {
                    Rule new_rule;
                    new_rule.non_terminal = non_terminal + '\'';
                    new_rule.prod_count = 0;

                    printf("%c -> %s%c'\n", non_terminal, common_prefix, new_rule.non_terminal);
                    
                    for (int m = 0; m < rules[i].prod_count; m++) {
                        if (strncmp(rules[i].productions[m], common_prefix, l) == 0) {
                            new_rule.productions[new_rule.prod_count] = malloc(MAX_LEN);
                            sprintf(new_rule.productions[new_rule.prod_count], "%s", rules[i].productions[m] + l);
                            new_rule.prod_count++;
                        }
                    }
                    new_rule.productions[new_rule.prod_count] = malloc(MAX_LEN);
                    sprintf(new_rule.productions[new_rule.prod_count], "ε");
                    new_rule.prod_count++;

                    rules[rule_count] = new_rule;
                    rule_count++;

                    break;
                }
            }
        }

        if (common_prefix[0] == '\0') {
            for (int j = 0; j < rules[i].prod_count; j++) {
                printf("%c -> %s\n", non_terminal, rules[i].productions[j]);
            }
        }
    }
}

int main() {
    Rule rules[MAX_RULES];
    int rule_count = 0;
    
    rules[rule_count].non_terminal = 'A';
    rules[rule_count].productions[0] = "ab";
    rules[rule_count].productions[1] = "ac";
    rules[rule_count].prod_count = 2;
    rule_count++;

    eliminate_left_factoring(rules, rule_count);
    return 0;
}
```
<img width="756" height="227" alt="check grammer" src="https://github.com/user-attachments/assets/aa18291a-6e5e-4110-b013-833eb653bee0" />





