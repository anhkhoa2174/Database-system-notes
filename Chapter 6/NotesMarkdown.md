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

- `ORDER BY`, `LIKE`

- `UPDATE`, `SET`, `INSERT INTO`, `DELETE FROM`
