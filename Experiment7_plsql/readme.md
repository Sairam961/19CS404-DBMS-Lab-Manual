# Experiment 7: PL/SQL – Variables, Control Structures and Loops

## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:
- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers

### Steps:
- Declare two numeric variables and initialize them.
- Use an `IF` statement to compare the values.
- Display the greater number using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Greater number is: 80

**Program:**
```
DECLARE
    num1 NUMBER := 50;
    num2 NUMBER := 80;
BEGIN
    IF num1 > num2 THEN
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num1);
    ELSE
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num2);
    END IF;
END;
/
```

**Output:**

<img width="1065" height="572" alt="image" src="https://github.com/user-attachments/assets/16d72118-ff6e-45f8-bd2a-5123fa094867" />

---

## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Sum of first 10 natural numbers is: 55

**Program::**
```
DECLARE
    n NUMBER := 10;
    sum NUMBER := 0;
    i NUMBER := 1;
BEGIN
    WHILE i <= n LOOP
        sum := sum + i;
        i := i + 1;
    END LOOP;
    DBMS_OUTPUT.PUT_LINE('Sum of first ' || n || ' natural numbers is: ' || sum);
END;
/
```

**Output:**

<img width="831" height="289" alt="image" src="https://github.com/user-attachments/assets/68cf51d3-acef-4ca4-9cad-f45a53c1f9fb" />

---

## 3. Write a PL/SQL program to generate Fibonacci series

### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.

**Expected Output:**  
n = 7  
Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8

**Program:**
```
DECLARE
    n NUMBER := 7;
    a NUMBER := 0;
    b NUMBER := 1;
    c NUMBER;
    i NUMBER;
    output_str VARCHAR2(100);
BEGIN
    DBMS_OUTPUT.PUT_LINE('n = ' || n);
    IF n >= 1 THEN
        output_str := TO_CHAR(a);
    END IF;
    IF n >= 2 THEN
        output_str := output_str || ', ' || TO_CHAR(b);
    END IF;
    FOR i IN 3..n LOOP
        c := a + b;
        output_str := output_str || ', ' || TO_CHAR(c);
        a := b;
        b := c;
    END LOOP;
    DBMS_OUTPUT.PUT_LINE('Fibonacci sequence: ' || output_str);
END;
/
```

**Output:**

<img width="680" height="313" alt="image" src="https://github.com/user-attachments/assets/8a586674-cbb1-4053-8184-2c31e7323a1a" />

---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

**Expected Output:**  
n = 1535  
Reversed number is 5351

**Program:**
```
DECLARE
    n NUMBER := 1535;
    temp NUMBER;
    rev NUMBER := 0;
    rem NUMBER;
BEGIN
    DBMS_OUTPUT.PUT_LINE('n = ' || n);
    temp := n;
    WHILE temp > 0 LOOP
        rem := MOD(temp, 10);
        rev := (rev * 10) + rem;
        temp := TRUNC(temp / 10);
    END LOOP;
    DBMS_OUTPUT.PUT_LINE('Reversed number is ' || rev);
END;
/
```

**Output:**

<img width="599" height="307" alt="image" src="https://github.com/user-attachments/assets/9512170b-17d0-4a4e-bfd0-0f4d00bdd1ab" />

---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.

**Expected Output:**  
a = 10, b = 9, c = 15  
Largest of three number is 15

**Program:**
```
DECLARE
    a NUMBER := 10;
    b NUMBER := 9;
    c NUMBER := 15;
    largest NUMBER;
BEGIN
    DBMS_OUTPUT.PUT_LINE('a = ' || a || ', b = ' || b || ', c = ' || c);
    IF a >= b THEN
        IF a >= c THEN
            largest := a;
        ELSE
            largest := c;
        END IF;
    ELSIF b >= c THEN
        largest := b;
    ELSE
        largest := c;
    END IF;
    DBMS_OUTPUT.PUT_LINE('Largest of three number is ' || largest);
END;
/
```

**Output:**

<img width="647" height="315" alt="image" src="https://github.com/user-attachments/assets/43a4932d-4ec9-4719-8172-10d396806f92" />

## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.
