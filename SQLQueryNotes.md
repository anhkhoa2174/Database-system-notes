CREATE USER c##testclc IDENTIFIED BY p123456;


GRANT DBA TO c##testclc; 

------------------------------------------------
CREATE TABLE EMPLOYEE
(
	SSN INT,
	FNAME CHAR(10)
)
------------------------------------------------
DROP TABLE EMPLOYEE (xóa table)
------------------------------------------------
SELECT FNAME, SALARY
FROM EMPLOYEE
WHERE FNAME = 'John' AND LNAME = 'Smith' (Condition sử dụng ' ', tên cột sử dụng " ")
;
------------------------------------------------
SELECT FNAME, LNAME, SALARY
FROM EMPLOYEE
WHERE LNAME <mark>LIKE</mark> '%English%' ( Tìm cả những người McEnglishTea, SuperEnglish,...) (Nếu chỉ là 'English' thì McEnglishTea, SuperEnglish,... không thỏa mà Tom English mới thỏa)
;
------------------------------------------------
SELECT FNAME, LNAME, SALARY
FROM EMPLOYEE
WHERE TRIM(LNAME)='English'  ( TRIM loại bỏ khoảng trắng thừ : '   English ' -> 'English'
;
------------------------------------------------
SELECT FNAME AS "FIRST NAME", LNAME, SALARY (as là đổi tên cột FNAME thành FIRST NAME)
FROM EMPLOYEE
WHERE TRIM(LNAME)='English'
;
------------------------------------------------
SELECT EMP.FNAME AS "FIRST NAME", LNAME, SALARY
FROM EMPLOYEE EMP
WHERE TRIM(LNAME)='English'
;
------------------------------------------------
(SSN, First Name, Project Name, Name of Managing Department)
SELECT SSN, FNAME AS "First Name", PNAME AS "Project Name", DNAME AS "Name of Managing Department"
FROM EMPLOYEE JOIN WORKS ON SSN = ESSN
JOIN PROJECT ON PNO = PNUMBER
JOIN DEPARTMENT ON DNUM = DNUMBER
;

------------------------------------------------
SELECT E.FNAME, E.LNAME, S.FNAME, S.LNAME
FROM EMPLOYEE AS E, EMPLOYEE AS S
WHERE E.SUPERSSN=S.SSN
(E là bí danh cho bảng EMPLOYEE thứ nhất.
S là bí danh cho bảng EMPLOYEE thứ hai.)
------------------------------------------------
ORDER BY SSN (sắp xếp theo cột SSN theo tứ tự tang dần; cùng ý nghĩa với ORDDER BY SSN ASC)
ORDER BY SSN DESC (giảm dần)
------------------------------------------------
|| : concatenate
------------------------------------------------
CASE
	WHEN +  ĐIỀU KIỆN ĐÚNG + THEN + ACTION
	ELSE +  ĐIỀU KIỆN SAI
END AS col (lưu giá trị vào cột này)

