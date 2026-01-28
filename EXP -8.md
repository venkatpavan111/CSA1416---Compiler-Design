```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_ENTRIES 100
#define MAX_NAME_LEN 50

typedef struct {
    char name[MAX_NAME_LEN];
    int value;
} Symbol;

typedef struct {
    Symbol table[MAX_ENTRIES];
    int count;
} SymbolTable;

void insert(SymbolTable *symTable, char *name, int value) {
    if (symTable->count < MAX_ENTRIES) {
        strcpy(symTable->table[symTable->count].name, name);
        symTable->table[symTable->count].value = value;
        symTable->count++;
    } else {
        printf("Symbol table is full.\n");
    }
}

int search(SymbolTable *symTable, char *name) {
    for (int i = 0; i < symTable->count; i++) {
        if (strcmp(symTable->table[i].name, name) == 0) {
            return symTable->table[i].value;
        }
    }
    return -1; // Not found
}

void delete(SymbolTable *symTable, char *name) {
    for (int i = 0; i < symTable->count; i++) {
        if (strcmp(symTable->table[i].name, name) == 0) {
            for (int j = i; j < symTable->count - 1; j++) {
                symTable->table[j] = symTable->table[j + 1];
            }
            symTable->count--;
            return;
        }
    }
    printf("Symbol not found.\n");
}

void display(SymbolTable *symTable) {
    for (int i = 0; i < symTable->count; i++) {
        printf("%s -> %d\n", symTable->table[i].name, symTable->table[i].value);
    }
}

int main() {
    SymbolTable symTable;
    symTable.count = 0;

    insert(&symTable, "x", 10);
    insert(&symTable, "y", 20);
    insert(&symTable, "z", 30);

    display(&symTable);

    printf("Searching for 'y': %d\n", search(&symTable, "y"));

    delete(&symTable, "x");

    display(&symTable);

    return 0;
}
```



<img width="655" height="372" alt="email" src="https://github.com/user-attachments/assets/4ac762bf-48eb-4c3f-8c56-ba5abf4015b4" />




