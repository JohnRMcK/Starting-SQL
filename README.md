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
