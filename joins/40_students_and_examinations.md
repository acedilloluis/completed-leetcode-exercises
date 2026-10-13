## Students And Examinations

### Problem Statement

Table: Students 

```sql
Create table If Not Exists Students (student_id int, student_name varchar(20))
```

student_id is the primary key (column with unique values) for this table.
Each row of this table contains the ID and the name of one student in the school.

Table: Subjects 

```sql
Create table If Not Exists Subjects (subject_name varchar(20))
```

subject_name is the primary key (column with unique values) for this table.
Each row of this table contains the name of one subject in the school.

Table: Examinations 

```sql
Create table If Not Exists Examinations (student_id int, subject_name varchar(20))
```

There is no primary key (column with unique values) for this table. It may contain duplicates.
Each student from the Students table takes every course from the Subjects table.
Each row of this table indicates that a student with ID student_id attended the exam of subject_name.

Write a solution to find the number of times each student attended each exam.
Return the result table ordered by student_id and subject_name.

### Solution

```sql
SELECT
    students.student_id,
    students.student_name,
    subjects.subject_name,
    COUNT(examinations.subject_name) AS attended_exams
FROM students
CROSS JOIN subjects
LEFT JOIN examinations
    ON students.student_id = examinations.student_id
        AND subjects.subject_name = examinations.subject_name
GROUP BY
    students.student_id,
    students.student_name,
    subjects.subject_name
ORDER BY
    students.student_id,
    students.student_name;
```

### Notes

#### Why use CROSS JOIN?
CROSS JOIN will return the Cartesian product of two tables. In this case, CROSS JOIN will match every row from the students table with every row from the subjects table. Since every student must take an exam for every subject in the subjects table, CROSS JOIN will add every subject_name to every student.

#### Explanation
 
The query will first CROSS JOIN the subjects table to the students table (see above for explanation for how CROSS JOIN works). Then, it will join the examinations table to the result of the CROSS JOIN. LEFT JOIN is used to fill columns with NULL where the student has not taken a particular exam. The rows are then grouped by student id, name, and subject name. For each tuple, the COUNT function is used to count the number of times that a particular subject name appears in the subject_name column of the examinations table, in other words, the number of times a student sat for that exam. The query then orders the results, in descending order, by student id and name. 