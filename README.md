# Starting-SQL
My first dive into learning SQL
all credit to freeCodeCamp.org and their $ hour intro to SQL video on youtube. 
CODE I MADE:


CREATE TABLE student (
    student_id INT PRIMARY KEY, /*primary key has to be NOT NULL and UNIQUE*/
    name VARCHAR (20) NOT NULL,
    major VARCHAR (20) DEFAULT 'Undeclared'

);

INSERT INTO student VALUES (1, 'Jack', 'Biology');

INSERT INTO student VALUES (2, 'Kate', 'Sociology');

INSERT INTO student(student_id, name) VALUES (3, 'Jebb'); /*When the major is unkonwn or not defined*/

INSERT INTO student VALUES (4, 'Teddy', 'Law');

INSERT INTO student VALUES (5, 'Mike', 'Comp Sci');

SELECT * FROM student;

DROP TABLE student


/*_________WITH AUTO INCREMENT________*/

CREATE TABLE student (
    student_id INT AUTO_INCREMENT PRIMARY KEY, /*primary key has to be NOT NULL and UNIQUE*/
    name VARCHAR (20) NOT NULL,
    major VARCHAR (20) DEFAULT 'Undeclared'

);

INSERT INTO student(name, major) VALUES ('Jack', 'Biology');

INSERT INTO student(name, major) VALUES ('Kate', 'Sociology');

INSERT INTO student(name) VALUES ('Jebb'); /*When the major is unkonwn or not defined*/

SELECT * FROM student;

DROP TABLE student

CREATE TABLE employee (
  emp_id INT PRIMARY KEY,
  first_name VARCHAR(40),
  last_name VARCHAR(40),
  birth_day DATE,
  sex VARCHAR(1),
  salary INT,
  super_id INT,
  branch_id INT
);

CREATE TABLE branch (
  branch_id INT PRIMARY KEY,
  branch_name VARCHAR(40),
  mgr_id INT,
  mgr_start_date DATE,
  FOREIGN KEY(mgr_id) REFERENCES employee(emp_id) ON DELETE SET NULL
);

ALTER TABLE employee
ADD FOREIGN KEY(branch_id)
REFERENCES branch(branch_id)
ON DELETE SET NULL;

CREATE TABLE client (
  client_id INT PRIMARY KEY,
  client_name VARCHAR(40),
  branch_id INT,
  FOREIGN KEY(branch_id) REFERENCES branch(branch_id) ON DELETE SET NULL
);

CREATE TABLE works_with (
  emp_id INT,
  client_id INT,
  total_sales INT,
  PRIMARY KEY(emp_id, client_id),
  FOREIGN KEY(emp_id) REFERENCES employee(emp_id) ON DELETE CASCADE,
  FOREIGN KEY(client_id) REFERENCES client(client_id) ON DELETE CASCADE
);

/*  Composite Key uses multipule keys    */

CREATE TABLE branch_supplier (
  branch_id INT,
  supplier_name VARCHAR(40),
  supply_type VARCHAR(40),
  PRIMARY KEY(branch_id, supplier_name),
  FOREIGN KEY(branch_id) REFERENCES branch(branch_id) ON DELETE CASCADE
);

INSERT INTO employee VALUES(100, 'David', 'Wallace', '1967-11-17', 'M', 250000, NULL, NULL);

INSERT INTO branch VALUES(1, 'Corporate', 100, '2006-02-09');

UPDATE employee
SET branch_id = 1
WHERE emp_id = 100;

INSERT INTO employee VALUES(101, 'Jan', 'Levinson', '1961-05-11', 'F', 110000, 100, 1);

INSERT INTO employee VALUES(102, 'Michael', 'Scott', '1964-03-15', 'M', 75000, 100, NULL);

INSERT INTO branch VALUES(2, 'Scranton', 102, '1992-04-06');

UPDATE employee
SET branch_id = 2
WHERE emp_id = 102;

INSERT INTO employee VALUES(103, 'Angela', 'Martin', '1971-06-25', 'F', 63000, 102, 2);
INSERT INTO employee VALUES(104, 'Kelly', 'Kapoor', '1980-02-05', 'F', 55000, 102, 2);
INSERT INTO employee VALUES(105, 'Stanley', 'Hudson', '1958-02-19', 'M', 69000, 102, 2);

INSERT INTO employee VALUES(106, 'Josh', 'Porter', '1969-09-05', 'M', 78000, 100, NULL);

INSERT INTO branch VALUES(3, 'Stamford', 106, '1998-02-13');

UPDATE employee
SET branch_id = 3
WHERE emp_id = 106;

INSERT INTO employee VALUES(107, 'Andy', 'Bernard', '1973-07-22', 'M', 65000, 106, 3);
INSERT INTO employee VALUES(108, 'Jim', 'Halpert', '1978-10-01', 'M', 71000, 106, 3);

INSERT INTO branch_supplier VALUES(2, 'Hammer Mill', 'Paper');
INSERT INTO branch_supplier VALUES(2, 'Uni-ball', 'Writing Utensils');
INSERT INTO branch_supplier VALUES(3, 'Patriot Paper', 'Paper');
INSERT INTO branch_supplier VALUES(2, 'J.T. Forms & Labels', 'Custom Forms');
INSERT INTO branch_supplier VALUES(3, 'Uni-ball', 'Writing Utensils');
INSERT INTO branch_supplier VALUES(3, 'Hammer Mill', 'Paper');
INSERT INTO branch_supplier VALUES(3, 'Stamford Lables', 'Custom Forms');

INSERT INTO client VALUES(400, 'Dunmore Highschool', 2);
INSERT INTO client VALUES(401, 'Lackawana Country', 2);
INSERT INTO client VALUES(402, 'FedEx', 3);
INSERT INTO client VALUES(403, 'John Daly Law, LLC', 3);
INSERT INTO client VALUES(404, 'Scranton Whitepages', 2);
INSERT INTO client VALUES(405, 'Times Newspaper', 3);
INSERT INTO client VALUES(406, 'FedEx', 2);

INSERT INTO works_with VALUES(105, 400, 55000);
INSERT INTO works_with VALUES(102, 401, 267000);
INSERT INTO works_with VALUES(108, 402, 22500);
INSERT INTO works_with VALUES(107, 403, 5000);
INSERT INTO works_with VALUES(108, 403, 12000);
INSERT INTO works_with VALUES(105, 404, 33000);
INSERT INTO works_with VALUES(107, 405, 26000);
INSERT INTO works_with VALUES(102, 406, 15000);
INSERT INTO works_with VALUES(105, 406, 130000);

/*  END OF COPY AND PASTED CODE    */

SELECT * FROM employee;
SELECT * FROM branch_supplier;-
SELECT * FROM client;
SELECT * FROM works_with;

/*  MORE BASIC QUERIES  */

SELECT * FROM employee ORDER BY salary DESC;

SELECT * FROM employee ORDER BY sex, last_name;

SELECT * FROM employee LIMIT 5;

SELECT first_name, last_name FROM employee;

SELECT first_name AS Forename, last_name as Surname FROM employee;
/*  Seems to re title columns for visual purposes    */

SELECT DISTINCT sex FROM employee;

SELECT DISTINCT branch_id FROM employee;

/*  Basic SQL Functions  */

SELECT COUNT(emp_id) from employee;
SELECT COUNT(super_id) from employee;

SELECT COUNT(emp_id) FROM employee WHERE sex = 'M' AND salary > '65000';

SELECT AVG(salary) FROM employee;
SELECT AVG(salary) FROM employee WHERE sex = 'M';

SELECT SUM(salary) from employee;

/* Aggregation  */
SELECT COUNT(sex), 
sex FROM employee
GROUP BY sex;

/* Wildcards and the LIKE function  */  

SELECT * from client WHERE client_name LIKE '%LLC';
/*  the percent sign is any number of characters while and underscore would represent one charcater   */

SELECT * FROM employee WHERE birth_day LIKE '____-11%';

SELECT first_name FROM employee UNION SELECT branch_name FROM branch;
/* must have the same sumber of columns and the same data type */

SELECT SUM(total_sales) FROM works_with
UNION
SELECT SUM(salary) FROM employee;

INSERT INTO branch VALUES(4, 'Buffalo', NULL, NULL);

-- find all branches and the name of their managers -- 
SELECT employee.emp_id, employee.first_name, branch.branch_name
FROM employee
JOIN branch
ON employee.emp_id = branch.mgr_id;
/* LEFT JOIN all results from top employee in this case table*/
SELECT employee.emp_id, employee.first_name, branch.branch_name
FROM employee
LEFT JOIN branch
ON employee.emp_id = branch.mgr_id;

SELECT employee.emp_id, employee.first_name, branch.branch_name
FROM employee
RIGHT JOIN branch
ON employee.emp_id = branch.mgr_id;

/*a full outer join would cobine a LEFT and RIGHT JOIN*/

/* NESTED QUERIES ---- Using the result of one select statment to inform the results of a subsequent SELECT statement. */

SELECT employee.first_name, employee.last_name FROM employee where employee.emp_id IN (
    SELECT works_with.emp_id FROM works_with WHERE works_with.total_sales > 30000
);

SELECT client.client_name FROM client WHERE client.branch_id = (
    SELECT branch.branch_id FROM branch WHERE branch.mgr_id = 102 LIMIT 1
);

/* ON DELETE set null -> will set values to null or cascade -> will delete associate columns
Primary keys cannot be a null value which is when we use ON DELETE CASCADE*/

/* DELIMITER is a special phrase in MySQL */

DELIMITER $$
CREATE
    TRIGGER my_trigger BEFORE INSERT
    ON employee
    FOR EACH ROW BEGIN
        INSERT INTO trigger_test VALUES ('added new emplpoyee');
    END$$
DELIMITER ;
