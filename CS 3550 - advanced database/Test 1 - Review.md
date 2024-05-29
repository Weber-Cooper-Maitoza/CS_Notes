LOOK AT ERD
- Know how to write a CREATE TABLE statement
```sql
CREATE TABLE Test (
	  sdTest_id     INT           NOT NULL IDENTITY(1, 1)
	, testName      NVARCHAR(255) NOT NULL
	, Blah          SMALLMONEY    NOT NULL
	, sdOther_id    INT           NOT NULL
);
```

- DROP TABLE STATEMENTS

- Know how to write a Primary Key statement using the ALTER TABLE statement
```sql
ALTER TABLE Test
	ADD CONSTRAINT PK_Test
	PRIMARY KEY (sdTest_id);
```

- Know how to write a Foreign Key statement using the ALTER TABLE statement
```sql
ALTER TABLE Test
	ADD CONSTRAINT FK_Test_Other
	FOREIGN KEY (sdOther_id) REFERENCES Other (sdOther_id);
```

- Know how to write an Alternate Key statement using the ALTER TABLE statement
```sql
ALTER TABLE Test
	ADD CONSTRAINT AK_Test
	UNIQUE (testName);
```

- Know how to write a Data Constraint statement using the ALTER TABLE statement
```sql
ALTER TABLE Vendor
	ADD CONSTRAINT CK_Vendor_zip
	CHECK (vendorZip LIKE '[0-9][0-9][0-9][0-9][0-9][0-9][0-9][0-9][0-9]'
		OR vendorZip LIKE '[0-9][0-9][0-9][0-9][0-9]');

ALTER TABLE Customer
	ADD CONSTRAINT CK_Customer_emailAddress
	CHECK (customerEmailAddress LIKE '%@%.%');
```

- Know how to write an INSERT statement
```sql
INSERT INTO Test(testName, blah) VALUE ('This is a test', 'blah');
INSERT INTO Test(testName, blah) VALUE ('This is a test', 'blah');
INSERT INTO Test(testName, blah) VALUE ('This is a test', 'blah');
INSERT INTO Test(testName, blah) VALUE ('This is a test', 'blah');
INSERT INTO Test(testName, blah) VALUE ('This is a test', 'blah');
```

