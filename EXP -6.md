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

void eliminate_left_recursion(Rule *rules, int rule_count) {
    for (int i = 0; i < rule_count; i++) {
        char non_terminal = rules[i].non_terminal;
        int alpha_count = 0, beta_count = 0;
        char *alpha[MAX_RULES], *beta[MAX_RULES];
        
        for (int j = 0; j < rules[i].prod_count; j++) {
            if (rules[i].productions[j][0] == non_terminal) {
                alpha[alpha_count++] = rules[i].productions[j] + 1;
            } else {
                beta[beta_count++] = rules[i].productions[j];
            }
        }

        if (alpha_count > 0) {
            Rule new_rule;
            new_rule.non_terminal = non_terminal + '\'';
            new_rule.prod_count = 0;

            for (int j = 0; j < beta_count; j++) {
                printf("%c -> %s%c'\n", non_terminal, beta[j], non_terminal);
            }
            for (int j = 0; j < alpha_count; j++) {
                new_rule.productions[new_rule.prod_count] = malloc(MAX_LEN);
                sprintf(new_rule.productions[new_rule.prod_count], "%s%c'", alpha[j], non_terminal);
                new_rule.prod_count++;
            }
            new_rule.productions[new_rule.prod_count] = malloc(MAX_LEN);
            sprintf(new_rule.productions[new_rule.prod_count], "ε");
            new_rule.prod_count++;

            rules[rule_count] = new_rule;
            rule_count++;
        } else {
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
    rules[rule_count].productions[0] = "Aa";
    rules[rule_count].productions[1] = "b";
    rules[rule_count].prod_count = 2;
    rule_count++;

    eliminate_left_recursion(rules, rule_count);
    return 0;
}
```
<img width="625" height="468" alt="identifier" src="https://github.com/user-attachments/assets/0d7f79ea-edb7-48f4-aa8b-4fc9754538bd" />


