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

### 3. Write a PL/SQL block to increase salary by 5000 for employees with emp_id > 101 and display the number of rows updated.
### 4. Write a PL/SQL block to retrieve employee name and salary for emp_id = 101 using SELECT INTO and display the result.
### 5. Write a PL/SQL block to update the salary of employee with emp_id = 102 by 3000. Display a message “Record Updated” if the row is found, otherwise display “Record Not Found”.
### 6. Write a PL/SQL block to delete the employee with emp_id = 999. Display a message “No Record Found” if no rows are deleted, otherwise display “Record Deleted” using SQL%NOTFOUND.
### 7. Write a PL/SQL block to display emp_name and salary of all employees using an explicit cursor.
### 8. Write a PL/SQL block to display employees whose salary is greater than 60000 using explicit cursor.
### 9. Write a PL/SQL block to count number of employees using explicit cursor and display the count using %ROWCOUNT.
### 10. Write a PL/SQL block to check whether a cursor is open or not using %ISOPEN.
### 11. Write a trigger to ensure that salary of an employee cannot be less than 30000 before inserting a record.
### 12. Write a trigger to display a message after inserting a new employee record.
### 13. Write a trigger to prevent updating salary to a value less than 30000.
### 14. Write a trigger to display the employee name before deleting the record.
