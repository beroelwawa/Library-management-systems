CREATE TABLE MEMBER (
    MemberID INT PRIMARY KEY,
    MemberName VARCHAR(100),
    Email VARCHAR(100),
    Phone VARCHAR(15)
);

CREATE TABLE AUTHOR (
    AuthorID INT PRIMARY KEY,
    AuthorName VARCHAR(100),
    Nationality VARCHAR(50)
);

CREATE TABLE LIBRARIAN (
    LibrarianID INT PRIMARY KEY,
    LibrarianName VARCHAR(100),
    Position VARCHAR(50)
);

CREATE TABLE LOANTRANSACTIONS (
    LoanID INT PRIMARY KEY,
    LoanDate DATE,
    ReturnDate DATE
);

CREATE TABLE BOOK (
    ISBN VARCHAR(13) PRIMARY KEY,
    Title VARCHAR(100),
    Category VARCHAR(50),
    Publisher VARCHAR(100),
    YearOfPublication INT,
    TotalCopiesAvailable INT,
    MemberID INT,
    AuthorID INT,
    LibrarianID INT,
    LoanID INT,
    FOREIGN KEY (MemberID) REFERENCES MEMBER(MemberID),
    FOREIGN KEY (AuthorID) REFERENCES AUTHOR(AuthorID),
    FOREIGN KEY (LibrarianID) REFERENCES LIBRARIAN(LibrarianID),
    FOREIGN KEY (LoanID) REFERENCES LOANTRANSACTIONS(LoanID)
);

INSERT INTO MEMBER VALUES
(1,'Ahmed Ali','ahmed@gmail.com','0501111111'),
(2,'Sara Khalid','sara@gmail.com','0502222222'),
(3,'Mona Salem','mona@gmail.com','0503333333');

INSERT INTO AUTHOR VALUES
(101,'Naguib Mahfouz','Egyptian'),
(102,'Ghazi Al Gosaibi','Saudi'),
(103,'Paulo Coelho','Brazilian');

INSERT INTO LIBRARIAN VALUES
(201,'Faisal Ahmed','Manager'),
(202,'Lama Ali','Assistant');

INSERT INTO LOANTRANSACTIONS VALUES
(301,'2026-01-10','2026-01-20'),
(302,'2026-02-15','2026-02-25');

INSERT INTO BOOK VALUES
('9780000000001','Database Systems','Technology','Pearson',2022,10,1,101,201,301),
('9780000000002','Computer Networks','Technology','McGraw Hill',2021,8,2,102,202,302),
('9780000000003','The Alchemist','Novel','HarperCollins',1988,15,3,103,201,301);

SELECT * FROM BOOK;

SELECT Title, Category
FROM BOOK;

SELECT *
FROM MEMBER;

SELECT *
FROM BOOK
WHERE Category = 'Technology';

UPDATE BOOK
SET TotalCopiesAvailable = 20
WHERE ISBN = '9780000000001';

DELETE FROM BOOK
WHERE ISBN = '9780000000003';

SELECT B.Title, A.AuthorName
FROM BOOK B
INNER JOIN AUTHOR A
ON B.AuthorID = A.AuthorID;

SELECT M.MemberName, B.Title
FROM MEMBER M
LEFT JOIN BOOK B
ON M.MemberID = B.MemberID;

SELECT M.MemberName, L.LibrarianName
FROM MEMBER M
CROSS JOIN LIBRARIAN L;

SELECT Category, COUNT(*) AS NumberOfBooks
FROM BOOK
GROUP BY Category;

SELECT *
FROM BOOK
ORDER BY YearOfPublication DESC;.
