# PL/SQL Lab Term Work Questions

###  1. Write a PL/SQL block to create a table Employees with columns emp_id, emp_name, and salary, and display a message using implicit cursor attributes.
Ans.   
Simple Rule:
- DML (INSERT, UPDATE, DELETE) → direct use allowed
- DDL (CREATE, DROP, ALTER) → EXECUTE IMMEDIATE required

```SQL
  BEGIN
      EXECUTE IMMEDIATE '
          CREATE TABLE Employees (
              emp_id NUMBER,
              emp_name VARCHAR2(50),
              salary NUMBER
          )';
  
      IF SQL%ROWCOUNT = 0 THEN
          DBMS_OUTPUT.PUT_LINE('Table created successfully.');
      END IF;
  END;
```


### 2. Write a PL/SQL block to insert 3 records into Employees table and display the number of rows inserted using implicit cursor.
Ans. 

```SQL
  BEGIN
      INSERT INTO Employees VALUES (1, 'Amit', 30000);
      INSERT INTO Employees VALUES (2, 'Rahul', 40000);
      INSERT INTO Employees VALUES (3, 'Neha', 35000);
  
      DBMS_OUTPUT.PUT_LINE('Rows inserted: ' || SQL%ROWCOUNT);
  END;
```

### 3. Write a PL/SQL block to increase salary by 5000 for employees with emp_id > 101 and display the number of rows updated.
Ans. 

```SQL
  BEGIN
      UPDATE Employees
      SET salary = salary + 5000
      WHERE emp_id > 101;
  
      DBMS_OUTPUT.PUT_LINE('Rows updated: ' || SQL%ROWCOUNT);
  END;
```

### 4. Write a PL/SQL block to retrieve employee name and salary for emp_id = 101 using SELECT INTO and display the result.
Ans. 

```SQL
  DECLARE
      v_name   Employees.emp_name%TYPE;
      v_salary Employees.salary%TYPE;
  BEGIN
      SELECT emp_name, salary
      INTO v_name, v_salary
      FROM Employees
      WHERE emp_id = 101;
  
      DBMS_OUTPUT.PUT_LINE('Name: ' || v_name || ', Salary: ' || v_salary);
  END;
```

### 5. Write a PL/SQL block to update the salary of employee with emp_id = 102 by 3000. Display a message “Record Updated” if the row is found, otherwise display “Record Not Found”.
Ans. 

```SQL
  BEGIN
      UPDATE Employees
      SET salary = salary + 3000
      WHERE emp_id = 102;
  
      IF SQL%ROWCOUNT > 0 THEN
          DBMS_OUTPUT.PUT_LINE('Record Updated');
      ELSE
          DBMS_OUTPUT.PUT_LINE('Record Not Found');
      END IF;
  END;
```

### 6. Write a PL/SQL block to delete the employee with emp_id = 999. Display a message “No Record Found” if no rows are deleted, otherwise display “Record Deleted” using SQL%NOTFOUND.
Ans. 

```SQL
  BEGIN
      DELETE FROM Employees
      WHERE emp_id = 999;
  
      IF SQL%NOTFOUND THEN
          DBMS_OUTPUT.PUT_LINE('No Record Found');
      ELSE
          DBMS_OUTPUT.PUT_LINE('Record Deleted');
      END IF;
  END;
```

### 7. Write a PL/SQL block to display emp_name and salary of all employees using an explicit cursor.
Ans. 

```SQL
  DECLARE
      CURSOR emp_cursor IS
          SELECT emp_name, salary FROM Employees;
  
      v_name   Employees.emp_name%TYPE;
      v_salary Employees.salary%TYPE;
  BEGIN
      OPEN emp_cursor;
      LOOP
          FETCH emp_cursor INTO v_name, v_salary;
          EXIT WHEN emp_cursor%NOTFOUND;
  
          DBMS_OUTPUT.PUT_LINE('Name: ' || v_name || ', Salary: ' || v_salary);
      END LOOP;
      CLOSE emp_cursor;
  END;
```

### 8. Write a PL/SQL block to display employees whose salary is greater than 60000 using explicit cursor.
Ans. 

```SQL
  DECLARE
      CURSOR emp_cursor IS
          SELECT emp_name, salary 
          FROM Employees 
          WHERE salary > 60000;
  
      v_name   Employees.emp_name%TYPE;
      v_salary Employees.salary%TYPE;
  BEGIN
      OPEN emp_cursor;
      LOOP
          FETCH emp_cursor INTO v_name, v_salary;
          EXIT WHEN emp_cursor%NOTFOUND;
  
          DBMS_OUTPUT.PUT_LINE('Name: ' || v_name || ', Salary: ' || v_salary);
      END LOOP;
      CLOSE emp_cursor;
  END;
```

### 9. Write a PL/SQL block to count number of employees using explicit cursor and display the count using %ROWCOUNT.
Ans. 

```SQL
  DECLARE
      CURSOR emp_cursor IS
          SELECT * FROM Employees;
  
      v_rec emp_cursor%ROWTYPE;
  BEGIN
      OPEN emp_cursor;
      LOOP
          FETCH emp_cursor INTO v_rec;
          EXIT WHEN emp_cursor%NOTFOUND;
      END LOOP;
  
      DBMS_OUTPUT.PUT_LINE('Number of employees: ' || emp_cursor%ROWCOUNT);
      CLOSE emp_cursor;
  END;
```

### 10. Write a PL/SQL block to check whether a cursor is open or not using %ISOPEN.
Ans. 

```SQL
  DECLARE
      CURSOR emp_cursor IS
          SELECT emp_name, salary FROM Employees;
  BEGIN
      IF emp_cursor%ISOPEN THEN
          DBMS_OUTPUT.PUT_LINE('Cursor is already open');
      ELSE
          DBMS_OUTPUT.PUT_LINE('Cursor is not open');
      END IF; 
      CLOSE emp_cursor;
  END;
```

### 11. Write a trigger to ensure that salary of an employee cannot be less than 30000 before inserting a record.
Ans. 

```SQL
  CREATE OR REPLACE TRIGGER trg_check_salary
  BEFORE INSERT ON Employees
  FOR EACH ROW
  BEGIN
      IF :NEW.salary < 30000 THEN
          RAISE_APPLICATION_ERROR(-20001, 'Salary cannot be less than 30000');
      END IF;
  END;
```

### 12. Write a trigger to display a message after inserting a new employee record.
Ans. 

```SQL
  CREATE OR REPLACE TRIGGER trg_after_insert_emp
  AFTER INSERT ON Employees
  FOR EACH ROW
  BEGIN
      DBMS_OUTPUT.PUT_LINE('New employee record inserted');
  END;
```

### 13. Write a trigger to prevent updating salary to a value less than 30000.
Ans. 

```SQL
  CREATE OR REPLACE TRIGGER trg_check_salary_update
  BEFORE UPDATE OF salary ON Employees
  FOR EACH ROW
  BEGIN
      IF :NEW.salary < 30000 THEN
          RAISE_APPLICATION_ERROR(-20002, 'Salary cannot be less than 30000');
      END IF;
  END;
```

### 14. Write a trigger to display the employee name before deleting the record.
Ans. 

```SQL
  CREATE OR REPLACE TRIGGER trg_before_delete_emp
  BEFORE DELETE ON Employees
  FOR EACH ROW
  BEGIN
      DBMS_OUTPUT.PUT_LINE('Deleting Employee: ' || :OLD.emp_name);
  END;
```
