# CSharp and SQL Fundamentals
01. What is the purpose of a `namespace`?

  > Namespace exports the file it calls so that other files are able to use it. It also allows for inheritance. This replaces the following method from Node:
    export class CatController extends BaseController

02. What is the difference between a `class` and an `interface`?

  > A class has a definition and is instantiated, whereas an interface only has a definition. This allows the interface to be read without it taking up any space in memory. Additionally, the interface is the container of methods that a class will be guaranteed to use.

03. What is the method that returns an instance of a class, yet it has no return type?

  > The constructor method returns and instance of a class without a return type. This allows us to supply default values and limit how often it can be instantiated.

04. There was no question 4 for us!

05. In the Car example what is the access modifier of the `Start()` method?

  ```c#
  abstract class Car
  {
    public string Start()
    {

      return "Vroooom";

    }
  }
  ```

  > public is the access modifier for Start(). This allows the Start method to be accessed by all classes.

06. In the Car example what is `string` an indication of?

  > "String" is the indication of the data type that the method is expecting to return back. Since C# is type based, it would throw an error if there wasn't a data type, or if the function returned a data type that wasn't a string.

07. In the Car example what is `abstract` preventing?

  > 'abstract' is preventing the Car example from having an object created of it. In order for this class to have objects created of it, it would need to be inherited from a different class.

08. In a SQL table, what is the difference between information in a row and information in a column?

  > The information in a row is each individual item that is stored in the database. This can be users, cars, houses, etc. A column contains the properties that the item can have, like email, picture, name, etc.

09. Demonstrate the necessary SQL for creating a table called `characters` with the values `name, age, description` as strings, and an `int` id.

  > CREATE TABLE
      users(
        id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
        name VARCHAR(255) NOT NULL,
        age SMALLINT UNSIGNED NOT NULL,
        description VARCHAR(255) NOT NULL,
      )

10. In SQL how can you query more than a single table? Provide an example.

  > When you query more than one table, you need to select multiple tables and then join them together. This will also only work correctly if you have the columns with these properties on the respective tables:
  > 
