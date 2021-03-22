> Refer : https://oracle-base.com/articles/8i/jserver-java-in-the-database


```sql
CREATE OR REPLACE AND COMPILE JAVA SOURCE NAMED "Mathematics" AS
import java.lang.*;
import java.sql.*;
import oracle.sql.*;
import oracle.jdbc.driver.*;

public class Mathematics
{
  
  public static int addNumbers (int Number1, int Number2)
  {
    try
    {
      int iReturn = -1;
      
      // Connect to the database
      Connection conn = null;
      OracleDriver ora = new OracleDriver(); 
      conn = ora.defaultConnection(); 
      
      // Check record exists, and create it if it doesn't
      Statement statement = conn.createStatement();
      ResultSet resultSet = statement.executeQuery("SELECT " + Number1 + " + " + Number2 + " FROM dual");
      if (resultSet.next())
      {
        iReturn = resultSet.getInt(1);
      }
      resultSet.close();
      statement.close();
      conn.close();

      return iReturn;
    }
    catch (Exception e)
    {
      return -1;
    }
  } 

};
/
```

show errors java source "Mathematics"
Publish the Java call specification
Once this Java class is compiled into the database you will need to publish a call specification for it's method. This involves writing a PL/SQL "Wrapper" to allow the method to be called from PL/SQL. The following code sample creates a function called Addition which publishes the Mathematics method Add.

```sql
CREATE OR REPLACE FUNCTION AddNumbers (p_number1  IN  NUMBER, p_number2  IN  NUMBER) RETURN NUMBER
AS LANGUAGE JAVA 
NAME 'Mathematics.addNumbers (int, int) return int';
/
```

Test It
We are now ready to use the Java class. The PL/SQL Wrapper allows it to be called from both SQL and PL/SQL.


```sql
SELECT addNumbers(1,2)
FROM   dual;

```
