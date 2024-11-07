# Notes of chapter 6

## Relational algebra

- **SELECT**

  > σ<sub>selection condition</sub>(R)  
  > SELECT is commutative.

- **PROJECT**

  > π<sub>column names</sub>(R)  
  > The project operation removes any duplicate tuples because the result of the project operation does not allow duplicate elements.  
  > PROJECT is not commutative.

- **RENAME**

  > ρ<sub>S(B1, B2, ..., Bn)</sub>(R) changes both the relation name to S, and the column (attribute) names to B1, B2, ..., Bn.  
  > ρ<sub>S</sub>(R) changes the relation name only to S.  
  > ρ<sub>(B1, B2, ..., Bn)</sub>(R) changes the column (attribute) names only to B1, B2, ..., Bn.

- **CARTESIAN PRODUCT**

  > R × S will combine every tuple of R with every tuple of S (R has n attributes and n<sub>S</sub> tuples; S has m attributes and n<sub>R</sub> tuples ).  
  > Result is a relation with degree n + m attributes, n<sub>S</sub> \* n<sub>R</sub> tuples.
  > **Example**:
  >
  > Let R =  
  > | A | B |  
  > |---|---|  
  > | 1 | 2 |  
  > | 3 | 4 |
  >
  > Let S =  
  > | C |  
  > |---|  
  > | 5 |  
  > | 6 |
  >
  > The Cartesian Product (R × S) will be:  
  > | A | B | C |  
  > |---|---|---|  
  > | 1 | 2 | 5 |  
  > | 1 | 2 | 6 |  
  > | 3 | 4 | 5 |  
  > | 3 | 4 | 6 |

- **EQUIJOIN**

  > R ⨝<sub>join condition</sub> S  
  > When the "join condition" is "=", it's called an **EQUIJOIN**.  
  > Example:

  > R(A, B, C)  
  > | A | B | C |  
  > |---|---|---|  
  > | 1 | 2 | 5 |  
  > | 3 | 4 | 7 |

  > S(C, D)  
  > | C | D |  
  > |---|---|  
  > | 5 | 9 |  
  > | 7 | 10 |

  > EQUIJOIN (R.C = S.C)  
  > | A | B | R.C | S.C | D |  
  > |---|---|-----|-----|----|  
  > | 1 | 2 | 5 | 5 | 9 |  
  > | 3 | 4 | 7 | 7 | 10 |

- **NATURAL JOIN**

  > The **NATURAL JOIN** operation, denoted by `*`, was created to get >rid of the second attribute in an EQUIJOIN condition.

  > Let R(A, B, C, D) and S(C, D, E) be two relations. The implicit join condition includes each pair of attributes with the same name, joined with an "AND":  
  > R.C = S.C AND R.D = S.D  
  > The result will keep only one attribute of each pair, so the result schema would be:

  > Result schema: (A, B, C, D, E)

  > Example tables:  
  > Let R =  
  > | A | B | C | D |  
  > |---|---|---|---|  
  > | 1 | 2 | 5 | 6 |  
  > | 3 | 4 | 7 | 8 |

  > Let S =  
  > | C | D | E |  
  > |---|---|---|  
  > | 5 | 6 | 9 |  
  > | 7 | 8 | 10 |

  > The **NATURAL JOIN** result (R \* S) will be:  
  > | A | B | C | D | E |  
  > |---|---|---|---|---|  
  > | 1 | 2 | 5 | 6 | 9 |  
  > | 3 | 4 | 7 | 8 | 10 |

  > Note: **NATURAL JOIN** chỉ giữ lại một phiên bản của mỗi cột trùng lặp (C và D).

## SQL commands

- When changing foreign key or the primary key, should the database refuse or have another option?

- Illustrates how a constraint may be given a constraint name, following the keyword `CONSTRAINT`.

- The same name can be used for two (or more) attributes as long as the attributes are in different tables.

- We could summarize any table by using the keyword `AS`.

- SQL usually treats a table not as a set but rather as a multiset.

- `UNION`, `EXCEPT`, `INTERSECT` require the same columns and the same datatype in each column.

- `SELECT` operator is used to select rows (horizontal partitions).

- `PROJECT` operator, denoted by π, is used to select columns (vertical partitions).

- The first feature allows comparison conditions on parts of a character string using the `LIKE` comparison operator.

- `BETWEEN`, `AND`, `OR`, `NOT`

- `ORDER BY`, `LIKE`. `ORDER BY` thì có ASC và DESC (mặc định không để gì la ASC)

- `UPDATE`, `SET`, `INSERT INTO`, `DELETE FROM`

# Thêm Constraints trong SQL

```sql
-- Thêm PRIMARY KEY CONSTRAINT
ALTER TABLE table_name
ADD CONSTRAINT constraint_name PRIMARY KEY (column_name);

-- Thêm FOREIGN KEY CONSTRAINT
ALTER TABLE table_name
ADD CONSTRAINT constraint_name FOREIGN KEY (column_name)
REFERENCES other_table_name(other_column_name);

-- Thêm CONSTRAINT CHECK hoặc UNIQUE
ALTER TABLE table_name
ADD CONSTRAINT constraint_name CHECK (condition);
ALTER TABLE table_name
ADD CONSTRAINT constraint_name UNIQUE (column_name);
Cascade với Referencing Key
markdown
Copy code
- ON DELETE CASCADE: Xóa bản ghi con khi bản ghi cha bị xóa.
- ON DELETE SET NULL: Đặt khóa ngoại thành NULL khi bản ghi cha bị xóa.
- ON DELETE RESTRICT: Ngăn chặn xóa bản ghi cha nếu có bản ghi con tham chiếu.
- ON DELETE NO ACTION: Tương tự RESTRICT, nhưng có thể trì hoãn.
- ON UPDATE CASCADE: Cập nhật bản ghi con khi bản ghi cha bị cập nhật.
- ON UPDATE SET NULL: Đặt khóa ngoại thành NULL khi bản ghi cha bị cập nhật.
- ON UPDATE SET DEFAULT: Đặt khóa ngoại về giá trị mặc định khi bản ghi cha bị cập nhật.
Cú pháp dành cho Function
sql
Copy code
CREATE OR REPLACE FUNCTION function_name 
    (parameter1 IN | OUT | IN OUT datatype, parameter2 IN | OUT | IN OUT datatype, ...)
RETURN return_datatype 
IS
    -- Biến cục bộ và khai báo (nếu cần)
BEGIN
    -- Logic và câu lệnh của hàm
    RETURN <giá trị trả về>;
EXCEPTION
    -- Xử lý ngoại lệ (nếu cần)
END function_name;
Cú pháp dành cho Stored Procedure
sql
Copy code
CREATE [OR REPLACE] PROCEDURE procedure_name
    (parameter_name [IN | OUT | IN OUT] datatype)
{IS | AS}
BEGIN
    procedure_body;
END procedure_name;
css
Copy code

Đoạn này sẽ giúp hiển thị code đẹp, liên tục và dễ đọc trong RMarkdown.
