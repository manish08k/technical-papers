# PostgreSQL Cheat Sheet

## 1. Terminal commands (at `%`)

```
psql                      # connect to default database
psql dbname               # connect to a database
psql -U user -d dbname    # connect as a user
createdb dbname           # create database
dropdb dbname             # delete database
pg_dump dbname > backup.sql        # backup
psql dbname < backup.sql           # restore
pg_dump -Fc dbname > backup.dump   # compressed backup
pg_restore -d dbname backup.dump   # restore compressed
```

## 2. psql commands (inside psql, no `;`)

```
\l                  list databases
\c dbname           switch database
\dt                 list tables
\dt+                list tables with size
\d table            describe table
\di                 list indexes
\dv                 list views
\df                 list functions
\dn                 list schemas
\du                 list users
\x                  toggle expanded output
\timing             show query time
\i file.sql         run a SQL file
\copy t FROM 'f.csv' CSV HEADER    import CSV
\copy t TO 'f.csv' CSV HEADER      export CSV
\e                  edit query in editor
\h CREATE TABLE     help on a SQL command
\?                  help on \ commands
\q                  quit
```

## 3. Database

```sql
CREATE DATABASE shop;
CREATE DATABASE shop OWNER manish;
DROP DATABASE shop;
ALTER DATABASE shop RENAME TO store;
```

## 4. Data types

```
int, bigint, smallint        whole numbers
serial, bigserial            auto-increment
numeric(10,2)                exact decimal
real, double precision       approximate decimal
text, varchar(n), char(n)    text
boolean                      true / false
date, time, timestamp, timestamptz, interval
uuid, jsonb, json
int[], text[]                arrays
```

## 5. Create / alter / drop table

```sql
CREATE TABLE students (
    id         serial PRIMARY KEY,
    name       text NOT NULL,
    email      text UNIQUE,
    age        int CHECK (age >= 0),
    city       text DEFAULT 'Bengaluru',
    created_at timestamp DEFAULT now()
);

CREATE TABLE IF NOT EXISTS t (...);
CREATE TABLE copy AS SELECT * FROM students;

ALTER TABLE students ADD COLUMN phone text;
ALTER TABLE students DROP COLUMN phone;
ALTER TABLE students RENAME COLUMN name TO full_name;
ALTER TABLE students RENAME TO pupils;
ALTER TABLE students ALTER COLUMN age TYPE bigint;
ALTER TABLE students ALTER COLUMN age SET NOT NULL;
ALTER TABLE students ALTER COLUMN age DROP NOT NULL;
ALTER TABLE students ALTER COLUMN city SET DEFAULT 'Delhi';
ALTER TABLE students ADD CONSTRAINT uq_email UNIQUE (email);
ALTER TABLE students ADD CONSTRAINT ck_age CHECK (age > 0);
ALTER TABLE students DROP CONSTRAINT uq_email;

DROP TABLE students;
DROP TABLE IF EXISTS students;
DROP TABLE students CASCADE;
TRUNCATE TABLE students;                       -- delete all rows
TRUNCATE TABLE students RESTART IDENTITY;      -- and reset ids
```

## 6. Constraints

```
PRIMARY KEY          unique + not null
NOT NULL             value required
UNIQUE               no duplicates
CHECK (condition)    custom rule
DEFAULT value        default value
FOREIGN KEY          link to another table
```

```sql
CREATE TABLE enrollments (
    id         serial PRIMARY KEY,
    student_id int REFERENCES students(id) ON DELETE CASCADE,
    course_id  int REFERENCES courses(id)  ON DELETE SET NULL,
    UNIQUE (student_id, course_id)
);
```

## 7. INSERT

```sql
INSERT INTO students (name, age) VALUES ('Asha', 20);
INSERT INTO students (name, age) VALUES ('Ravi', 21), ('Meera', 19);
INSERT INTO students (name, age) SELECT name, age FROM old_students;
INSERT INTO students (name) VALUES ('Zed') RETURNING id;
INSERT INTO students (email, name) VALUES ('a@x.com', 'A')
    ON CONFLICT (email) DO NOTHING;
INSERT INTO students (email, name) VALUES ('a@x.com', 'A')
    ON CONFLICT (email) DO UPDATE SET name = EXCLUDED.name;
```

## 8. UPDATE

```sql
UPDATE students SET age = 22 WHERE id = 2;
UPDATE students SET age = age + 1, city = 'Delhi' WHERE id = 3;
UPDATE students SET age = age + 1 RETURNING *;
UPDATE students s SET city = c.city FROM cities c WHERE c.id = s.city_id;
```

## 9. DELETE

```sql
DELETE FROM students WHERE id = 1;
DELETE FROM students WHERE age < 18;
DELETE FROM students WHERE id = 5 RETURNING *;
DELETE FROM students;                -- deletes ALL rows
```

## 10. SELECT

```sql
SELECT * FROM students;
SELECT name, age FROM students;
SELECT name AS student_name FROM students;
SELECT DISTINCT city FROM students;
SELECT name, age * 2 AS double_age FROM students;

SELECT   columns
FROM     table
WHERE    row_filter
GROUP BY columns
HAVING   group_filter
ORDER BY columns
LIMIT n OFFSET m;
```

## 11. WHERE operators

```sql
WHERE age = 20
WHERE age <> 20              -- also !=
WHERE age > 18 AND city = 'Delhi'
WHERE age < 18 OR age > 60
WHERE NOT age > 18
WHERE age BETWEEN 18 AND 25
WHERE city IN ('Delhi', 'Mumbai')
WHERE city NOT IN ('Delhi')
WHERE name LIKE 'A%'         -- starts with A
WHERE name LIKE '%a'         -- ends with a
WHERE name LIKE '%sh%'       -- contains sh
WHERE name LIKE '_s%'        -- 2nd letter s
WHERE name ILIKE 'asha'      -- case-insensitive
WHERE name ~ '^A.*a$'        -- regex
WHERE email IS NULL
WHERE email IS NOT NULL
WHERE age = ANY (ARRAY[18, 20])
```

## 12. ORDER BY / LIMIT

```sql
ORDER BY age
ORDER BY age DESC
ORDER BY city, age DESC
ORDER BY age DESC NULLS LAST
LIMIT 5
LIMIT 10 OFFSET 20
FETCH FIRST 5 ROWS ONLY
```

## 13. Aggregates / GROUP BY / HAVING

```sql
COUNT(*)   COUNT(col)   COUNT(DISTINCT col)
SUM(col)   AVG(col)     MIN(col)   MAX(col)
STRING_AGG(name, ', ')        ARRAY_AGG(name)

SELECT city, COUNT(*) AS total, AVG(age)
FROM students
WHERE age >= 18
GROUP BY city
HAVING COUNT(*) > 5
ORDER BY total DESC;

GROUP BY ROLLUP (a, b)
GROUP BY CUBE (a, b)
```

## 14. Joins

```sql
SELECT s.name, c.title
FROM students s
INNER JOIN enrollments e ON e.student_id = s.id
INNER JOIN courses c     ON c.id = e.course_id;

LEFT JOIN        -- all left rows + matches
RIGHT JOIN       -- all right rows + matches
FULL OUTER JOIN  -- all rows from both
CROSS JOIN       -- every combination
JOIN ... USING (id)                -- when column names match
NATURAL JOIN                       -- auto-match same names (avoid)

-- no match (anti-join)
SELECT s.* FROM students s
LEFT JOIN enrollments e ON e.student_id = s.id
WHERE e.id IS NULL;

-- self join
SELECT e.name, m.name AS manager
FROM employees e LEFT JOIN employees m ON m.id = e.manager_id;
```

## 15. Subqueries / EXISTS / CTE

```sql
SELECT * FROM students WHERE age > (SELECT AVG(age) FROM students);
SELECT * FROM students WHERE id IN (SELECT student_id FROM enrollments);
SELECT * FROM students s
 WHERE EXISTS (SELECT 1 FROM enrollments e WHERE e.student_id = s.id);
SELECT * FROM students s
 WHERE NOT EXISTS (SELECT 1 FROM enrollments e WHERE e.student_id = s.id);
SELECT * FROM (SELECT city, COUNT(*) n FROM students GROUP BY city) t WHERE n > 2;

WITH city_stats AS (
    SELECT city, COUNT(*) AS total FROM students GROUP BY city
)
SELECT * FROM city_stats WHERE total > 3;

WITH RECURSIVE chain AS (
    SELECT id, manager_id FROM employees WHERE manager_id IS NULL
    UNION ALL
    SELECT e.id, e.manager_id FROM employees e JOIN chain c ON e.manager_id = c.id
)
SELECT * FROM chain;
```

## 16. Set operations

```sql
SELECT a FROM t1 UNION SELECT a FROM t2;        -- no duplicates
SELECT a FROM t1 UNION ALL SELECT a FROM t2;    -- keep duplicates
SELECT a FROM t1 INTERSECT SELECT a FROM t2;
SELECT a FROM t1 EXCEPT SELECT a FROM t2;
```

## 17. CASE / NULL functions

```sql
CASE WHEN age < 18 THEN 'minor'
     WHEN age < 60 THEN 'adult'
     ELSE 'senior' END

CASE city WHEN 'Delhi' THEN 'N' WHEN 'Mumbai' THEN 'W' ELSE 'other' END

COALESCE(email, 'none')        -- first non-NULL
NULLIF(a, b)                   -- NULL if a = b
GREATEST(a, b, c)   LEAST(a, b, c)
```

## 18. Text functions

```sql
UPPER(s)  LOWER(s)  INITCAP(s)  LENGTH(s)
TRIM(s)  LTRIM(s)  RTRIM(s)
CONCAT(a, b)   a || b
SUBSTRING(s FROM 1 FOR 3)   SUBSTR(s, 1, 3)
LEFT(s, 3)   RIGHT(s, 3)
REPLACE(s, 'a', 'b')
POSITION('x' IN s)
SPLIT_PART('a,b,c', ',', 2)
LPAD(s, 5, '0')   RPAD(s, 5, '0')
REPEAT('ab', 3)   REVERSE(s)
REGEXP_REPLACE(s, '[0-9]', '', 'g')
FORMAT('%s is %s', a, b)
```

## 19. Number functions

```sql
ROUND(3.14159, 2)   CEIL(3.2)   FLOOR(3.8)   TRUNC(3.9)
ABS(-5)   MOD(10, 3)   POWER(2, 3)   SQRT(16)
RANDOM()                       -- 0 to 1
```

## 20. Date and time

```sql
NOW()   CURRENT_DATE   CURRENT_TIME   CURRENT_TIMESTAMP
EXTRACT(YEAR FROM d)   EXTRACT(MONTH FROM d)   EXTRACT(DOW FROM d)
DATE_TRUNC('month', d)
d + INTERVAL '7 days'
d - INTERVAL '1 month'
AGE(d1, d2)
d1 - d2                          -- days between dates
TO_CHAR(d, 'DD-Mon-YYYY')
TO_DATE('09-11-2026', 'DD-MM-YYYY')
d::date
```

## 21. Casting

```sql
CAST('42' AS int)
'42'::int
'2026-11-09'::date
123::text
```

## 22. Window functions

```sql
ROW_NUMBER() OVER (PARTITION BY city ORDER BY age DESC)
RANK()       OVER (PARTITION BY city ORDER BY age DESC)
DENSE_RANK() OVER (ORDER BY age DESC)
NTILE(4)     OVER (ORDER BY age)
LAG(col)     OVER (ORDER BY d)
LEAD(col)    OVER (ORDER BY d)
FIRST_VALUE(col) OVER (PARTITION BY g ORDER BY d)
LAST_VALUE(col)  OVER (PARTITION BY g ORDER BY d
                       ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)
SUM(col) OVER (ORDER BY d)                        -- running total
AVG(col) OVER (ORDER BY d ROWS BETWEEN 2 PRECEDING AND CURRENT ROW)
COUNT(*) OVER (PARTITION BY city)

-- top 1 per group
SELECT * FROM (
  SELECT *, ROW_NUMBER() OVER (PARTITION BY city ORDER BY age DESC) rn
  FROM students) t
WHERE rn = 1;
```

## 23. Indexes

```sql
CREATE INDEX idx_city ON students(city);
CREATE UNIQUE INDEX idx_email ON students(email);
CREATE INDEX idx_multi ON students(city, age);
CREATE INDEX idx_lower ON students(LOWER(name));
CREATE INDEX idx_partial ON students(city) WHERE age > 18;
DROP INDEX idx_city;
REINDEX TABLE students;

EXPLAIN SELECT ...;
EXPLAIN ANALYZE SELECT ...;
VACUUM ANALYZE students;
```

## 24. Views

```sql
CREATE VIEW adults AS SELECT * FROM students WHERE age >= 18;
CREATE OR REPLACE VIEW adults AS SELECT ...;
DROP VIEW adults;

CREATE MATERIALIZED VIEW stats AS SELECT city, COUNT(*) FROM students GROUP BY city;
REFRESH MATERIALIZED VIEW stats;
DROP MATERIALIZED VIEW stats;
```

## 25. Transactions

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;        -- save
ROLLBACK;      -- undo

SAVEPOINT sp1;
ROLLBACK TO sp1;
```

## 26. Functions, procedures, triggers

```sql
CREATE FUNCTION add(a int, b int) RETURNS int AS $$
    SELECT a + b;
$$ LANGUAGE SQL;

CREATE OR REPLACE FUNCTION set_updated() RETURNS trigger AS $$
BEGIN
    NEW.updated_at = now();
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trg_updated
BEFORE UPDATE ON students
FOR EACH ROW EXECUTE FUNCTION set_updated();

DROP TRIGGER trg_updated ON students;
DROP FUNCTION add(int, int);
```

## 27. JSON

```sql
SELECT data->'name'          FROM t;     -- as json
SELECT data->>'name'         FROM t;     -- as text
SELECT data->'a'->>'b'       FROM t;
SELECT * FROM t WHERE data @> '{"role":"admin"}';
SELECT jsonb_build_object('a', 1, 'b', 2);
SELECT jsonb_array_elements(data->'items') FROM t;
```

## 28. Arrays

```sql
SELECT ARRAY[1,2,3];
SELECT tags[1] FROM t;
SELECT * FROM t WHERE 'sql' = ANY(tags);
SELECT UNNEST(tags) FROM t;
SELECT ARRAY_AGG(name) FROM students;
```

## 29. Users and permissions

```sql
CREATE USER manish WITH PASSWORD 'secret';
CREATE ROLE readonly;
ALTER USER manish WITH PASSWORD 'new';
ALTER USER manish WITH SUPERUSER;
GRANT SELECT, INSERT, UPDATE, DELETE ON students TO manish;
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO manish;
GRANT ALL PRIVILEGES ON DATABASE shop TO manish;
REVOKE INSERT ON students FROM manish;
DROP USER manish;
```

## 30. Schemas and misc

```sql
CREATE SCHEMA sales;
SET search_path TO sales, public;
SELECT current_database(), current_user, version();
SELECT pg_size_pretty(pg_database_size('shop'));
SELECT pg_size_pretty(pg_total_relation_size('students'));

COMMENT ON TABLE students IS 'student records';
CREATE SEQUENCE my_seq START 1;
SELECT nextval('my_seq');
SELECT setval('students_id_seq', 100);

SELECT * FROM information_schema.tables WHERE table_schema = 'public';
SELECT * FROM information_schema.columns WHERE table_name = 'students';
```

## 31. Quick syntax rules

```
SQL statements end with ;       \ commands do not
Text uses 'single quotes'       "double quotes" are for identifiers
-- single-line comment          /* multi-line comment */
Prompt =#  ready                Prompt -#  unfinished (type ; or Ctrl+C)
```
