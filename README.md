#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>

#define MAX 100

int stack[MAX];
int top = -1;

// Push operation
void push(int value) {
    if (top == MAX - 1) {
        printf("Stack Overflow\n");
        return;
    }
    stack[++top] = value;
}

// Pop operation
int pop() {
    if (top == -1) {
        printf("Stack Underflow\n");
        return -1;
    }
    return stack[top--];
}

// Function to evaluate postfix expression
int evaluatePostfix(char exp[]) {
    int i = 0;
    char ch;
    int val1, val2;

    while (exp[i] != '\0') {
        ch = exp[i];

        // If operand, push to stack
        if (isdigit(ch)) {
            push(ch - '0');  // Convert char to int
        }
        else {
            val2 = pop();
            val1 = pop();

            switch (ch) {
                case '+': push(val1 + val2); break;
                case '-': push(val1 - val2); break;
                case '*': push(val1 * val2); break;
                case '/': push(val1 / val2); break;
            }
        }
        i++;
    }
    return pop();
}

int main() {
    char exp[MAX];

    printf("Enter Postfix Expression: ");
    scanf("%s", exp);

    int result = evaluatePostfix(exp);

    printf("Result = %d\n", result);

    return 0;
} 
