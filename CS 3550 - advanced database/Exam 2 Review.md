- Know how to create a STORE PROCEDURE if given an INSERT statement. You must be able to create variables that the user can input values (as an example the user would insert a first and last name and not a numeric key value for a user)
```sql
CREATE PROCEDURE dbo.udp_addUser
    @firstName    NVARCHAR(255)
  , @lastName     NVARCHAR(255)

AS BEGIN
  AS TRY
    INSERT INTO Users (firstName, lastName) Values (@firstName, @lastName);
  END TRY
  AS CATCH
    PRINT 'The INSERT INTO Users failed for ' +
    'firstName = ' + @firstName +
    ' lastName = ' + @lastName +
    ' ERROR MESSAGE: ' + ERROR_MESSAGE();
  END CATCH
END
GO
```

- Know how to create a Function when given a SELECT statement that calls a Primary Key value
```sql
CREATE FUNCTION [dbo].udf_Something (@emailAddress NVARCHAR(255))
RETURNS INT

AS BEGIN
  DECLARE @primaryKey INT;
  
  SELECT primaryKey
  FROM table
  WHERE emailAddress = @emailAddress

  IF @primaryKey IS NULL
  SET @primaryKey = -1
  RETURN @primaryKey
END
GO
```

- Know how to call a Function within a STORED PROCEDURE
```sql
CREATE PROCEDURE dbo.udp_procedureWithFunction
    @firstName      NVARCHAR(255)
  , @lastName       NVARCHAR(255)
  , @emailAddress   NVARCHAR(255)

AS BEGIN 
  AS TRY
    INSERT INTO Users (id, firstname, lastname) 
    VALUES ([dbo].udf_Something(@emailAddress)
           , @firstName
           , @lastName);
  END TRY
  AS CATCH
    PRINT 'THAT DIDNT WORK'
  END CATCH
END
GO
```
