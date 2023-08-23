# A bit more CSharp and SQL
1. What does ***inheritance*** accomplish for us in C#?

  > Inheritance allows for easier storage of data between models in C#. It can encapsulate away data that we don't want users to see, like an account email, while allowing us to use other properties between classes that we want to reuse.

2. How does ***member inheritance*** work in C#? Does a `Class` inherit all members of the base `Class`?

  > The derived class will inherit all members of the base class, except for its constructor. However, you can also add new members to the derived class that don't exist on the base class. This would be like an Account having an Email, but it inheriting the Id, Picture, and Name from the Profile.

3. How does ***accessibility*** affect inheritance?

  > If a member is marked as private, it will not be inherited by the derived class. However, public members will be.

4. What is the difference between a `PRIMARY KEY` and a `FOREIGN KEY`

  > A primary key is the key that identifies a new object within a table. This is created when the object is created, according to the table (INT, VARCHAR, etc.). A foreign key points to a member on an object that belongs to a different table. We use these in cases where we intend to use a virtual on an object. For example, a primary key on an account may be the account's id. Then, in a recipe we will use a foreign key to say that the creatorId is pointing to the id on the accounts table.

5. What is an ***alias***?

  > An alias is another name that you assign a namespace. It allows for easier importing and changing of the namespace.

6. Demonstrate how you would query a join statement that would get all of a doctors patients from the following collections:

  ```SQL
  CREATE TABLE doctors (
    id INT NOT NULL AUTO_INCREMENT,
    -- CODE OMITTED
    PRIMARY KEY (id)
  )

  CREATE TABLE patients (
    id INT NOT NULL AUTO_INCREMENT,
    -- CODE OMITTED
    PRIMARY KEY (id)
  )

  CREATE TABLE patient_doctors (
    id INT NOT NULL AUTO_INCREMENT,
    doctorId INT NOT NULL,
    patientId INT NOT NULL,

    FOREIGN KEY (doctorId)
      REFERENCES doctors(id),
    FOREIGN KEY (patientId)
      REFERENCES patients(id),
  )

  ```

  > 
