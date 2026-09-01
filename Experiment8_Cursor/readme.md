# Experiment 8: PL/SQL Cursor Programs

## AIM
To write and execute PL/SQL programs using cursors and exception handling to manage runtime errors effectively and display appropriate messages.

## THEORY

In PL/SQL, cursors are used to handle query result sets row-by-row. 

There are two types of cursors:

- Implicit Cursors: Automatically created by PL/SQL for single-row queries.
- Explicit Cursors: Declared and controlled by the programmer for multi-row queries.

Types of Explicit Cursors:

1. Simple Cursor: Basic cursor to iterate over multiple rows.

2. Parameterized Cursor: Accepts parameters to filter the result dynamically.

3. Cursor FOR Loop: Simplifies cursor operations (open, fetch, close).

4. %ROWTYPE Cursor: Fetches entire row into a record using %ROWTYPE.

5. Cursor with FOR UPDATE: Used for row-level locking and updating the rows while looping.

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

**Exception Handling**

PL/SQL provides a robust mechanism to handle runtime errors using exception handling blocks. When an error occurs during execution, control is passed to the EXCEPTION section, where specific or general errors can be handled gracefully.

### Components of Exception Handling:
- Predefined Exceptions: Automatically raised by PL/SQL for common errors (e.g., NO_DATA_FOUND, TOO_MANY_ROWS, ZERO_DIVIDE).
- User-defined Exceptions: Declared explicitly in the declaration section using the EXCEPTION keyword.
- WHEN OTHERS: A generic handler for all exceptions not handled explicitly.

```sql
BEGIN
   -- Statements
EXCEPTION
   WHEN exception_name THEN
      -- Handling code
   WHEN OTHERS THEN
      -- Handling for unknown errors
END;
```

### **Question 1: Simple Cursor with Exception Handling**

**Write a PL/SQL program using a simple cursor to fetch employee names and designations from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: When no rows are fetched.
2. **OTHERS**: Any other unexpected errors during execution.

**Steps:**

- Create an `employees` table with fields `emp_id`, `emp_name`, and `designation`.
- Insert some sample data into the table.
- Use a simple cursor to fetch and display employee names and designations.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

**Output:**  
The program should display the employee details or an error message.

**Program:**
```
DECLARE
    CURSOR c_std IS
        SELECT name, dept FROM students;
    v_name students.name%TYPE;
    v_dept students.dept%TYPE;
    v_count NUMBER := 0;
BEGIN
    OPEN c_std;
    LOOP
        FETCH c_std INTO v_name, v_dept;
        EXIT WHEN c_std%NOTFOUND;
        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('Name: ' || v_name || ', Dept: ' || v_dept);
    END LOOP;
    CLOSE c_std;
    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Error: No data found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: An unexpected error occurred.');
END;
/
```

**Result:**

<img width="611" height="360" alt="image" src="https://github.com/user-attachments/assets/eb5dee1a-9212-4952-be69-4e3090775140" />

---

### **Question 2: Parameterized Cursor with Exception Handling**

**Write a PL/SQL program using a parameterized cursor to retrieve and display employees with a salary in a given range. Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees meet the salary criteria.
2. **OTHERS**: For any unexpected errors during the execution.

**Steps:**

- Modify the `employees` table by adding a `salary` column.
- Insert sample salary values for the employees.
- Use a parameterized cursor to accept a salary range as input and fetch employees within that range.
- Implement exception handling to catch and display relevant error messages.

**Output:**  
The program should display the employee details within the specified salary range or an error message if no data is found.

**Program:**
```
DECLARE
    CURSOR c_std_marks (p_min NUMBER, p_max NUMBER) IS
        SELECT name, marks FROM students WHERE marks BETWEEN p_min AND p_max;
    v_name students.name%TYPE;
    v_marks students.marks%TYPE;
    v_count NUMBER := 0;
BEGIN
    OPEN c_std_marks(50, 90);
    LOOP
        FETCH c_std_marks INTO v_name, v_marks;
        EXIT WHEN c_std_marks%NOTFOUND;
        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('Name: ' || v_name || ', Marks: ' || v_marks);
    END LOOP;
    CLOSE c_std_marks;
    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Error: No students meet the marks criteria.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: An unexpected error occurred.');
END;
/
```

**Result:**

<img width="826" height="307" alt="image" src="https://github.com/user-attachments/assets/5aa21f46-ba8b-49c9-8c59-720e989d3e8b" />


---

### **Question 3: Cursor FOR Loop with Exception Handling**

**Write a PL/SQL program using a cursor FOR loop to retrieve and display all employee names and their department numbers from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no employees are found in the database.
2. **OTHERS**: For any other unexpected errors.

**Steps:**

- Modify the `employees` table by adding a `dept_no` column.
- Insert sample department numbers for employees.
- Use a cursor FOR loop to fetch and display employee names along with their department numbers.
- Implement exception handling to catch the relevant exceptions.

**Output:**  
The program should display employee names with their department numbers or the appropriate error message if no data is found.

**Program:**
```
DECLARE
    CURSOR c_dept IS
        SELECT name, dept FROM students;
    v_count NUMBER := 0;
BEGIN
    FOR rec IN c_dept LOOP
        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('Name: ' || rec.name || ', Dept: ' || rec.dept);
    END LOOP;
    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Error: No students found in the database.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: An unexpected error occurred.');
END;
/
```

**Result:**

<img width="628" height="372" alt="image" src="https://github.com/user-attachments/assets/683cc16f-e25e-42cd-9abf-14202908e430" />

---

### **Question 4: Cursor with `%ROWTYPE` and Exception Handling**

**Write a PL/SQL program that uses a cursor with `%ROWTYPE` to fetch and display complete employee records (emp_id, emp_name, designation, salary). Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees are found in the database.
2. **OTHERS**: For any other errors that occur.

**Steps:**

- Modify the `employees` table by adding `emp_id`, `emp_name`, `designation`, and `salary` fields.
- Insert sample data into the `employees` table.
- Declare a cursor using `%ROWTYPE` to fetch complete rows from the `employees` table.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

**Output:**  
The program should display employee records or the appropriate error message if no data is found.

**Program:**
```
DECLARE
    CURSOR c_std IS
        SELECT * FROM students;
    v_std_rec students%ROWTYPE;
    v_count NUMBER := 0;
BEGIN
    OPEN c_std;
    LOOP
        FETCH c_std INTO v_std_rec;
        EXIT WHEN c_std%NOTFOUND;
        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('Roll: ' || v_std_rec.roll || ', Name: ' || v_std_rec.name || ', Dept: ' || v_std_rec.dept || ', Marks: ' || v_std_rec.marks);
    END LOOP;
    CLOSE c_std;
    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Error: No students found in the database.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: An unexpected error occurred.');
END;
/
```

**Result:**

<img width="660" height="373" alt="image" src="https://github.com/user-attachments/assets/163bd316-5876-4fae-bdd5-fde9a61621ab" />

---

### **Question 5: Cursor with FOR UPDATE Clause and Exception Handling**

**Write a PL/SQL program using a cursor with the `FOR UPDATE` clause to update the salary of employees in a specific department. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no rows are affected by the update.
2. **OTHERS**: For any unexpected errors during execution.

**Steps:**

- Modify the `employees` table to include a `dept_no` and `salary` field.
- Insert sample data into the `employees` table with different department numbers.
- Use a cursor with the `FOR UPDATE` clause to lock the rows of employees in a specific department and update their salary.
- Implement exception handling to handle `NO_DATA_FOUND` or other errors that may occur.

**Output:**  
The program should update employee salaries and display a message, or it should display an error message if no data is found.

**Program:**
```
DECLARE
    CURSOR c_std_update IS
        SELECT marks FROM students WHERE dept = 'CS' FOR UPDATE;
    v_marks students.marks%TYPE;
    v_count NUMBER := 0;
BEGIN
    OPEN c_std_update;
    LOOP
        FETCH c_std_update INTO v_marks;
        EXIT WHEN c_std_update%NOTFOUND;
        v_count := v_count + 1;
        UPDATE students SET marks = marks + 5 WHERE CURRENT OF c_std_update;
    END LOOP;
    CLOSE c_std_update;
    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    ELSE
        DBMS_OUTPUT.PUT_LINE('Marks updated successfully for department CS.');
    END IF;
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Error: No rows were affected by the update.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: An unexpected error occurred.');
END;
/
```

**Result:**

<img width="728" height="302" alt="image" src="https://github.com/user-attachments/assets/bb0981d2-87ed-4ffa-810c-27dcd7e72d7d" />

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 

