# Relational Algebra Practice Worksheet

The following problems involve multi-operation expressions that involve
some of the following relational algebraic operations:

* Selection ($\sigma$)
* Projection ($\pi$)
* Union ($\cup$)
* Set difference (-)
* Intersection ($\cap$)
* Cartesian product ($\times$)
* Theta-join ($\bowtie_\theta$)
* Natural join ($\bowtie$)
* Renaming ($\rho$)

## Instructions

For each problem:

1. Evaluate the relational algebra expression.
2. Show intermediate results when the expression contains multiple operations.
3. Unless otherwise specified, assume relations contain **sets of tuples**.
4. For joins, clearly identify the attributes in the resulting relation.


# Part I — Selection

## Problem 1 — Simple Selection

Given:

**STUDENT(StudentID, Name, Major, GPA)**

| StudentID | Name  | Major   | GPA |
| --------: | ----- | ------- | --: |
|       101 | Alice | CS      | 3.8 |
|       102 | Bob   | Math    | 3.2 |
|       103 | Carol | CS      | 3.5 |
|       104 | David | Physics | 2.9 |
|       105 | Eve   | CS      | 3.9 |

Compute: $\sigma_{Major='CS'}(STUDENT)$

## Problem 2 — Selection with AND

Using the same `STUDENT` relation, compute: $\sigma_{Major='CS'\land GPA\geq3.7}(STUDENT)$

## Problem 3 — Selection with OR

Compute: $\sigma_{Major='Math'\lor Major='Physics'}(STUDENT)$

# Part II — Projection

## Problem 4 — Simple Projection

Using `STUDENT`, compute: $\pi_{Name,Major}(STUDENT)$

## Problem 5 — Projection with Duplicate Values

Consider:

**ENROLLMENT(StudentID, CourseID, Semester)**

| StudentID | CourseID | Semester |
| --------: | -------- | -------- |
|       101 | CS101    | Fall     |
|       102 | CS101    | Fall     |
|       103 | CS101    | Spring   |
|       101 | CS102    | Spring   |
|       104 | CS101    | Spring   |

Compute: $\pi_{CourseID}(ENROLLMENT)$

**Question:** Why does the answer contain fewer tuples than the original relation?

# Part III — Combining Selection and Projection

## Problem 6

Using `STUDENT`, compute:

$$
\pi_{Name,GPA}
\left(
\sigma_{Major='CS'}(STUDENT)
\right)
$$

## Problem 7

Compute:

$$
\pi_{Name}
\left(
\sigma_{GPA\geq3.5}(STUDENT)
\right)
$$

# Part IV — Union

Consider:

**CS_STUDENTS(StudentID, Name)**

| StudentID | Name  |
| --------: | ----- |
|       101 | Alice |
|       102 | Bob   |
|       103 | Carol |

**HONORS_STUDENTS(StudentID, Name)**

| StudentID | Name  |
| --------: | ----- |
|       103 | Carol |
|       104 | David |
|       105 | Eve   |

## Problem 8

Compute:

CS_STUDENTS $\cup$ HONORS_STUDENTS

## Problem 9

How would the result change if the two relations had different schemas?

For example:

CS_STUDENTS(StudentID,Name)

and

HONORS_STUDENTS(StudentID,GPA)

Can these relations be directly unioned? Explain.

# Part V — Set Difference

## Problem 10

Using the relations from Problems 8–9, compute:

$$
CS\_STUDENTS - HONORS\_STUDENTS
$$

Then compute:

HONORS_STUDENTS-CS_STUDENTS

What is the difference between the two results?


# Part VI — Intersection

## Problem 11

Compute:

CS_STUDENTS $\cap$ HONORS_STUDENTS

What does the result represent in this example?

## Problem 12 — Intersection Using Difference

Show that:

$$
R\cap S = R-(R-S)
$$

Use the following relations to verify the identity.

**R(A)**

|  A |
| -: |
|  1 |
|  2 |
|  3 |
|  4 |

**S(A)**

|  A |
| -: |
|  3 |
|  4 |
|  5 |

# Part VII — Cartesian Product

## Problem 13

Consider:

**STUDENT(StudentID, Name)**

| StudentID | Name  |
| --------: | ----- |
|       101 | Alice |
|       102 | Bob   |
|       103 | Carol |

**COURSE(CourseID, Title)**

| CourseID | Title      |
| -------- | ---------- |
| CS101    | Database   |
| CS102    | Algorithms |

Compute:

$$
STUDENT\times COURSE
$$

## Problem 14

If relation (R) contains 5 tuples and relation (S) contains 8 tuples:

$$
|R\times S|=?
$$

If (R) has 3 attributes and (S) has 4 attributes, how many attributes does $R\times S$ have?

# Part VIII — Theta-Join

## Problem 15

Compute:

$$
R \bowtie_{R.A < S.B} S
$$

**R(A, B)**

|  A |  B |
| -: | -: |
|  1 |  5 |
|  4 |  6 |
|  7 |  2 |

**S(B, C)**

|  B |  C |
| -: | -: |
|  3 | 10 |
|  5 | 20 |
|  8 | 30 |

## Problem 16

Compute:

$$
R\bowtie_{\substack{R.A>S.B \wedge R.B=S.C}}S
$$

**R(A, B)**

|  A |  B |
| -: | -: |
|  1 |  2 |
|  3 |  4 |
|  5 |  6 |

**S(B, C, D)**

|  B |  C |  D |
| -: | -: | -: |
|  2 |  4 |  6 |
|  4 |  6 |  8 |
|  4 |  7 |  9 |


# Part IX — Equijoin

## Problem 17

Compute:

$$
STUDENT\bowtie_{STUDENT.StudentID=ENROLLMENT.StudentID}ENROLLMENT
$$

**STUDENT(StudentID, Name)**

| StudentID | Name  |
| --------: | ----- |
|       101 | Alice |
|       102 | Bob   |
|       103 | Carol |

**ENROLLMENT(StudentID, CourseID)**

| StudentID | CourseID |
| --------: | -------- |
|       101 | CS101    |
|       101 | CS102    |
|       103 | CS101    |
|       104 | CS103    |

Which enrollment tuple does not participate in the join?

# Part X — Natural Join

## Problem 18

Compute:

$$
STUDENT\bowtie ENROLLMENT
$$

**STUDENT(StudentID, Name)**

| StudentID | Name  |
| --------: | ----- |
|       101 | Alice |
|       102 | Bob   |
|       103 | Carol |

**ENROLLMENT(StudentID, CourseID)**

| StudentID | CourseID |
| --------: | -------- |
|       101 | CS101    |
|       101 | CS102    |
|       103 | CS101    |

How is the result different from the Cartesian product?

## Problem 19 — Natural Join Warning

Consider:

**EMPLOYEE(EmpID, Name, DeptID)**

**DEPARTMENT(DeptID, Name)**

What happens if we compute:

$$
EMPLOYEE\bowtie DEPARTMENT
$$

Which attributes are used to match tuples?

What potential problem is caused by both relations having an attribute named `Name`?

# Part XI — Rename

## Problem 20

Consider:

**EMPLOYEE(EmpID, Name, ManagerID)**

| EmpID | Name  | ManagerID |
| ----: | ----- | --------: |
|     1 | Alice |         3 |
|     2 | Bob   |         3 |
|     3 | Carol |      NULL |

We want to compare an employee with their manager.

Use the rename operator to create:

$$
MANAGER=\rho_{M(EmpID,Name,ManagerID)}(EMPLOYEE)
$$

Then explain why renaming is necessary before joining `EMPLOYEE` with `MANAGER`.

# Part XII — Self-Join

## Problem 21

Using the `EMPLOYEE` relation from Problem 20, write a relational algebra expression that produces:

| Employee | Manager |
| -------- | ------- |
| Alice    | Carol   |
| Bob      | Carol   |

Hint: Rename one copy of `EMPLOYEE` before performing the join.

# Part XIII — Multi-Operation Expressions

## Problem 22

Using `STUDENT`, compute:

$$
\pi_{Name}
\left(
\sigma_{GPA>3.5}
(STUDENT)
\right)
$$

Write the intermediate relation after the selection.

## Problem 23

Using `STUDENT` and `ENROLLMENT`, find the names of students enrolled in `CS101`.

Use relational algebra involving:

* selection,
* join,
* projection.

## Problem 24

Find the names of CS students with GPA at least 3.5 who are enrolled in `CS101`.

Your expression should contain at least:

* selection,
* join,
* projection.

# Part XIV — More Challenging Queries

Consider the following database.

### STUDENT

| StudentID | Name  | Major   | GPA |
| --------: | ----- | ------- | --: |
|       101 | Alice | CS      | 3.8 |
|       102 | Bob   | Math    | 3.2 |
|       103 | Carol | CS      | 3.5 |
|       104 | David | Physics | 2.9 |
|       105 | Eve   | CS      | 3.9 |

### COURSE

| CourseID | Title      | Department |
| -------- | ---------- | ---------- |
| CS101    | Database   | CS         |
| CS102    | Algorithms | CS         |
| MATH201  | Calculus   | Math       |
| PHY101   | Physics    | Physics    |

### ENROLLMENT

| StudentID | CourseID |
| --------: | -------- |
|       101 | CS101    |
|       101 | CS102    |
|       102 | MATH201  |
|       103 | CS101    |
|       104 | PHY101   |
|       105 | CS101    |
|       105 | CS102    |

## Problem 25

Find the names of all students enrolled in at least one CS course.

## Problem 26

Find the names of students who are **not enrolled in any CS course**.

Hint: Consider using set difference.

## Problem 27

Find the names of CS majors who are enrolled in `CS101`.

## Problem 28

Find the names of students who have a GPA greater than 3.5 and are enrolled in `CS102`.

# Part XVI — Translate English into Relational Algebra

For each question, write a relational algebra expression.

## Problem 29

Find all students whose GPA is greater than 3.5.


## Problem 30

Find the names of all CS majors.


## Problem 31

Find the names and majors of students whose GPA is at least 3.5.


## Problem 32

Find students who are CS majors **or** Math majors.


## Problem 33

Find students who are CS majors **and** have a GPA greater than 3.5.


## Problem 34

Find students who are CS majors but are **not enrolled in CS101**.


## Problem 35

Find the names of students enrolled in CS101.


## Problem 36

Find the names of students enrolled in **both** CS101 and CS102.


## Problem 37

Find the students who are enrolled in **every required CS course**.

# Part XVII — Challenge Problems

## Problem 38 — Equivalent Expressions

Determine whether the following two expressions are equivalent:

$$
\sigma_{GPA>3.5\land Major='CS'}(STUDENT)
$$

and

$$
\sigma_{GPA>3.5}
\left(
\sigma_{Major='CS'}(STUDENT)
\right)
$$

Explain your answer.


## Problem 39 — Rewrite Without Join

Rewrite:

$$
R\bowtie_{\theta}S
$$

using only:

* Cartesian product
* selection

## Problem 40 — Rewrite Intersection

Rewrite:

$$
R\cap S
$$

using only:

* set difference
* other basic relational algebra operations.
