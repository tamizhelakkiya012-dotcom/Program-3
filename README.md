# Program-3# Infix Expression Evaluation using Stack

def apply_operator(op, b, a):
    if op == '+':
        return a + b
    if op == '-':
        return a - b
    if op == '*':
        return a * b
    if op == '/':
        return a / b

def precedence(op):
    if op == '+' or op == '-':
        return 1
    if op == '*' or op == '/':
        return 2
    return 0

def evaluate_infix(expression):
    operands = []
    operators = []

    for ch in expression:
        if ch.isdigit():
            operands.append(int(ch))
        elif ch in "+-*/":
            while operators and precedence(operators[-1]) >= precedence(ch):
                op = operators.pop()
                b = operands.pop()
                a = operands.pop()
                operands.append(apply_operator(op, b, a))
            operators.append(ch)

    while operators:
        op = operators.pop()
        b = operands.pop()
        a = operands.pop()
        operands.append(apply_operator(op, b, a))

    return operands[0]

expr = input("Enter infix expression (single digit operands): ")
result = evaluate_infix(expr)
print("Result of the expression is:", result)
output:
Enter infix expression (single digit operands): 2+3*4
Result of the expression is: 14
