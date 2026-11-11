
# Normalization in DBMS

Normalization is the process of organizing data in database tables to reduce duplicate data and avoid problems when inserting, updating or deleting records.

It usually involves splitting a large table into smaller related tables and connecting them using primary keys and foreign keys.

## Why do we need Normalization?

Suppose we store student and course details in a single table.

| student_id | student_name | course |
|---|---|---|
| 1 | Rahul | Python |
| 1 | Rahul | SQL |
| 2 | Priya | Python |

Here, Rahul's name is repeated because he enrolled in multiple courses.

If we have thousands of students and courses, storing repeated information makes the database difficult to maintain.

Normalization helps organize this data properly.

## 1. First Normal Form (1NF)

A table is in 1NF when:
- Each column contains a single value.
- There are no multiple values stored in one cell.
- Each row can be uniquely identified.

**Example (Not in 1NF):**

| student_id | name | courses |
|---|---|---|
| 1 | Rahul | Python, SQL |
| 2 | Priya | Java, C |

Here, the courses column contains multiple values in a single cell.

**After applying 1NF:**

| student_id | name | course |
|---|---|---|
| 1 | Rahul | Python |
| 1 | Rahul | SQL |
| 2 | Priya | Java |
| 2 | Priya | C |

Now each cell contains only one value.

## 2. Second Normal Form (2NF)

A table is in 2NF when:
- It is already in 1NF.
- Every non-key column must depend on the whole candidate key, not just part of a composite key.

**Example:**

Consider a table with a composite primary key (`student_id`, `course_id`).

| student_id | course_id | student_name | course_name |
|---|---|---|---|
| 1 | 101 | Rahul | Python |
| 1 | 102 | Rahul | SQL |
| 2 | 101 | Priya | Python |

Here:
- `student_name` depends only on `student_id`.
- `course_name` depends only on `course_id`.

These are partial dependencies because the columns depend on only part of the composite key.

**After applying 2NF:**

Students table:

| student_id | student_name |
|---|---|
| 1 | Rahul |
| 2 | Priya |

Courses table:

| course_id | course_name |
|---|---|
| 101 | Python |
| 102 | SQL |

Enrollments table:

| student_id | course_id |
|---|---|
| 1 | 101 |
| 1 | 102 |
| 2 | 101 |

Now each non-key column depends on the complete key of its table.

## 3. Third Normal Form (3NF)

A table is in 3NF when:
- It is already in 2NF.
- There should be no transitive dependency of non-key columns on a candidate key.

In simple words, non-key columns should depend on the key, the whole key and nothing but the key.

**Example:**

| employee_id | employee_name | department_id | department_name |
|---|---|---|---|
| 1 | Rahul | 101 | IT |
| 2 | Priya | 102 | HR |
| 3 | Arjun | 101 | IT |

Here:
- `employee_id` determines `department_id`.
- `department_id` determines `department_name`.

So, `department_name` indirectly depends on `employee_id` through `department_id`.

This is called transitive dependency.

**After applying 3NF:**

Employees table:

| employee_id | employee_name | department_id |
|---|---|---|
| 1 | Rahul | 101 |
| 2 | Priya | 102 |
| 3 | Arjun | 101 |

Departments table:

| department_id | department_name |
|---|---|
| 101 | IT |
| 102 | HR |

Now department details are stored separately instead of being repeated for every employee.

## 4. Boyce-Codd Normal Form (BCNF)

BCNF is a stricter version of 3NF.

A table is in BCNF when every determinant must be a superkey.

In simple words, whenever one column or a group of columns determines another column, the determining columns should be capable of uniquely identifying a row.

**Example:**

Consider a table:

| student | subject | teacher |
|---|---|---|
| Rahul | Python | Kumar |
| Priya | Python | Kumar |
| Rahul | SQL | Ramesh |

Suppose:
- Each student can study multiple subjects.
- Each subject has only one teacher.
- The combination of student and subject uniquely identifies a row.

Here, `subject` determines `teacher`, but `subject` is not a superkey because multiple students can study the same subject.

This violates BCNF.

We can split the table into:

Student_Subject table:

| student | subject |
|---|---|
| Rahul | Python |
| Priya | Python |
| Rahul | SQL |

Subject_Teacher table:

| subject | teacher |
|---|---|
| Python | Kumar |
| SQL | Ramesh |

Now subject and teacher details are stored separately.

## Benefits of Normalization

- Reduces duplicate data.
- Makes database maintenance easier.
- Prevents insertion, update and deletion anomalies.
- Improves data consistency.
- Makes relationships between tables clearer.
