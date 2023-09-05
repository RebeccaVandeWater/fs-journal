# SQL

#NOTE - SQL => Structured Query Database
#NOTE - ORM => Object Relational Model (mongoose[json script] to MongoDB[bson script], or dapper[C#] to MySQL)

#SECTION - Getting Started

1. In dbSetup.sql, click "Execute" in order to create a new table (the initial one will be about accounts, definitely spin that one up)
  - The new table will pop up in tables in the Database that you are using in the VSCode tab.
  - Make sure you finish writing the table first!

2. To create data in the database, you will write a statement underneath your tables:
  - INSERT INTO 
    capybaras(name, ownedByGrandma, birthday, applesEaten)
    VALUES ('Cappy', true, '1990-12-24', 1000);

3. To retrieve data from the database, you will write a statement underneath your INSERT methods:
  - SELECT name FROM capybaras; > This will give the specified column from the specified table.
  - You can stack which columns you get back:
    SELECT name, applesEaten FROM capybaras;
  - You can get all columns from that table:
    SELECT * FROM capybaras;
  - You can get ONE thing back from the database, like a FIND method:
    SELECT * FROM capybaras WHERE id = 2;
  - You can do the same thing, but for a property:
    SELECT * FROM capybaras WHERE applesEaten > 4;
    SELECT * FROM capybaras WHERE name LIKE '%tip%' > returns Tippy Toes because its name is LIKE 'tip'

4. To delete data from the database, typically underneath SELECT methods:
  - DELETE FROM capybaras WHERE id = 2;

5. To update the TABLE and add or take away a column, write:
  ALTER TABLE capybaras
  ADD 
  livesAtFarm BOOLEAN NOT NULL DEFAULT FALSE; > When you alter a column, it would be good practice to add a default so that previously added data has that value. Particularly when it has NOT NULL set on it.

  You can also:
  DROP TABLE capybaras > this will delete the table, then you can rewrite your table and then re-Execute it.

#STUB - SQL File Tour
- dbSetup.sql, the inital table will create an accounts table if one doesn't already exist. This is specified in nearly plain English in the code.
  - The name of the table is in the Create Table line.
  - Each line of code within the Create Table method is a new column in the table
  - varchar is a string, VARCHAR(255) means that a string of 255 bytes (or roughly 255 characters) can be stored in the column
  - The primary key in the table always has to be unique as it is the main identifier of the item in the table in the db. This is equivalent to _id in MongoDB. It cannot be null and it cannot be identical to a different primary key
  - You can leave comments on all of your columns in the table. This isn't necessary but is a helpful guide for yourself for the schema. It also gives more intellicense on what the column is made for.
  - You can create a default value on the column as well (the createdAt and updatedAt is a good reference for this)
  - ON UPDATE will automatically update the value whenever the item is updated.
  - default charset is the default font that the table will adhere to in the SQL database.

#TODO - Practice SQL syntax on SQLBolt (bookmarked in Chrome)

#SECTION - Syntax
  - The conventions of SQL table syntax is that you lowercase the column name and completely uppercase the SQL properties on that column
  - Add a semicolon at the end of the table 
  - INT points to an integer
  - NOT NULL means that the item cannot be null in the database
  - AUTO_INCREMENT means that the id's will automatically increment in the database, so that they are always unique and they will not need a complicated id.
  - To write a default value, you can write something like BOOLEAN DEFAULT true.
  - SMALLINT UNSIGNED says how big the integer can be (how many bytes can be stored) and UNSIGNED states that it has to be a positive number
  - ENUM is the type for enums, and in order to create them you would write them like this:
    - category ENUM('misc', 'cats', 'dogs', 'gachamon', 'games') DEFAULT 'misc'
  - TEXT is another type of VARCHAR, but has a massive character count.

#SECTION - Using SQL data in C#

#STUB - Getting Started
  1. Go to appsettings.Development.json and insert the CONNECTION STRING from the MySQL database in ScaleGrid
    - This will be the Master Connection String
    - Make sure the ID is the same as the sample user that you have created in your database
    - Slack the file contents to yourself to ensure that you have the right one easy to find each time!
  
#STUB - Writing the back end in C#
  1. Write a model out for your database item. You will not need to create a constructor for the model because it will be cast in by the database. You will only need to create the properties on the model.
    - The properties should match the way that you set up the SQL model.
    - Don't forget to use the prop stub to make writing out the properties easier!
  
  2. Make a new API Controller for the database item. 

  3. Make a new Service for the database item.
    - Register the Service in the Startup file!

  4. Make a new Repository for the database item.
    - Register the Repository in the Startup file!
  
  5. Write your Get method!
    In the Controller:
      private readonly CarsService _carsService;

      public CarsController(CarsService carsService)
      {
        _carsService = carsService;
      }

      [HttpGet]

      public ActionResult<List<Car>> GetCars()
      {
        try
        {
          List<Car> cars = _carsService.GetCars();
          return Ok(cars);
        }
        catch(Exception e)
        {
          return BadRequest(e.Message);
        }
      }

    In the Service:
      private readonly CarsRepository _carsRepository;

      public CarsService(CarsRepository carsRepository)
      {
        _carsRepository = carsRepository
      }

      internal List<Car> GetCars()
      {
        List<Car> cars = _carsRepository.GetCars();
        return Ok(cars);
      }
    
    In the Repository:
      private readonly IDbConnection _db; > This is the connection between our ORM (Dapper) and our database (MySQL)

      public CarsRepository(IDbConnection db)
      {
        _db = db
      }

      internal List<Car> GetCars()
      {
        string sql = "SELECT * FROM cars;"; > This is writing SQL inside C#. It should look exactly the same as how you would write the syntax in a .sql file

        List<Car> cars = _db.Query<Car>(sql).ToList(); > This is a Dapper query for the cars, which would normally return an array. We need to convert it to a List so that the data can be manipulated more easily

        return cars
      }

  6. Write a Get by ID!
    In the Controller:

      [HttpGet("{carId}")]

      public ActionResult<Car> GetCarById(int ) > Note that this is not a List, just a Car! Also, note how the parameters are passed in
      {
        try
        {
          Car car = _carsService.GetCarById(carId);
          return Ok(car)
        }
        catch(Exception e)
        {
          return BadRequest(e.Message)
        }
      }

    In the Service:
      internal Car GetCarById(int carId)
      {
        Car car = _carsRepository.GetCarById(carId);

        if(car == null)
        {
          throw new Exception($"{carId} is not a valid Id")
        }

        return car;
      }

    In the Repository:
      internal Car GetCarById(int carId)
      {
        string sql = $"SELECT * FROM cars WHERE id = {carId};"; **THIS IS BAD** This allows users to pass strings that they write which can return or delete whatever information they wish. This only works if you're passing through a string, but you should instead parameterize the information like below to sanitize the data.

        string sql = "SELECT * FROM cars WHERE id - @carId"

        Car car = _db.QueryFirstOrDefault<Car>(sql, new {carId}); > This will return the first result or null if it doesn't find anything. This is the same as FindById in mongoose. However, this is also the sanitization explained above. This creates a new object that will be queried for, and it should match the parameter that you're passing in the wrapping function.

        return car;
      }

  7. Write your Post request!
    In your Controller:

      [HttpPost]

      public ActionResult<Car> CreateCar([FromBody] Car carData) > This automatically casts the carData into a new Car.
      {
        try
        {
          Car car = _carsService.CreateCar(carData);
          return Ok(car)
        }
        catch(Exception e)
        {
          return BadRequest(e.Message)
        }
      }

    In your Service:
      internal Car CreateCar(Car carData)
      {
        int carId = _carsRepository.CreateCar(carData);

        Car car = Get car GetCarById(carId);

        return car;
      }

    In your Repository:

      internal int CreateCar(Car carData)
      {
        string sql = @" > The @ sign makes it multi-line
        INSERT INTO cars (make, model, year, price, color, ownedByGrandma)
        VALUES(@Make, @Model, @Year, @Price, @Color, @OwnedByGrandma); > These are the values that we will pass through, like in SQL, but is protected by passing in these items as parameters with the @ symbol
        SELECT LAST_INSERT_ID > This grabs that object that was just inserted, which is only returned as a number (the ID) in SQL
        ;"; > This entire string passes in two SQL commands. We can run however many we want, but do keep in mind that best practices are to encapsulate code appropriately.

        int carId = _db.ExecuteScalar<int>(sql, carData); > This says to run the code affected and return back the ID. The object is the carData in this case.

        <!-- carData.Id = carId; > This attaches the carId that was just made to the carData that was sent down. It's not great, but does work and serve the purpose we want. -->

        return carId;
      }

  8. Write your delete method!

    In your Controller:

      [HttpDelete("{carId}")]

      public ActionResult<string> RemoveCar(int carId)
      {
        try
        {
          Car car = _carsService.RemoveCar(carId);

          return Ok($"{car.Make} {car.Model} was deleted.");
        }
        catch()
        {

        }
      }

    In the Service:
      internal void RemoveCar(int carId) > We're not expecting anything to be returned because it will be deleted.
      {
        car Car = GetCarById(carId)

        _carsRepository.RemoveCar(carId)
      }

    In the Repository:
      internal void RemoveCar(int carId)
      {
        string sql = "DELETE FROM cars WHERE id = @carId LIMIT 1;";

        _db.Execute(sql, new {carId});
      }

  9. Write your Put request!

    In the Controller:
      [HttpPut("{carId}")]

      public ActionResult<Car> UpdateCar(int carId, [FromBody] Car carData)
      {
        try
        {
          Car car = _carsService.UpdateCar(carId, carData);
          return Ok(car);
        }
      }

    In the Service:
      internal Car UpdateCar(int carId, Car carData)
      {
        Car originalCar = GetCarById(carId);

        originalCar.Make = carData.Make ?? originalCar.Make; > This is a better null check than an elvis operator or an OR operator
        originalCar.Model = carData.Model ?? originalCar.Model;
        originalCar.Color = carData.Color ?? originalCar.Color;

        > These are technically not nullable values, because they are a number or bool and it might be intended to be something like 0. So, you have to make these values nullable in the Model.
        originalCar.Price = carData.Price ??  originalCar.Price; 
        originalCar.Year = carData.Year ?? originalCar.Year;
        originalCar.OwnedByGrandma = carData.OwnedByGrandma ?? originalCar.OwnedByGrandma;

        Car car = _carsRepository.UpdateCar(originalCar);
        return car;
      }

    In the Repository:
      internal Car UpdateCar(Car originalCar)
      {
        string sql = @"
        UPDATE cars SET
        make = @Make,
        model = @Model,
        color = @Color,
        year = @Year,
        price = @Price, 
        ownedByGrandma = @OwnedByGrandma
        WHERE id = @Id > There is no dot notation. Dapper looks through the object you send in and finds these properties for you.
        LIMIT 1;
        SELECT * FROM cars WHERE id = @Id
        ;";

        Car updatedCar =  _db.QueryFirstOrDefault<Car>(sql, originalCar);

        return updatedCar;
      }

#SECTION - Building a Full Stack Application with C# and SQL

#STUB - Getting Started
  1. When creating your folder, use bcw createe > dotnet vue

  2. Initialize the repository before opening the Workspace

  3. Make sure your database is connected with the correct Connection String and User

  4. Hook up your connection information in the appsettings.Development.json file
    - The auth0 domain and audience will be the same as the ones used previously in Vue full stack applications.

  5. Fill in the same information in the .env file in the front end
    - Make sure that the .env file has the correct port (should be 7045 or something similar)
    - Make sure that the same port also has https instead of http

  6. Spin up the client and the server (localhost:8080 is still the client side URL)

#STUB - One to Many Relationships
  * In this example, we're going to create a creatorId on an album. This references the id on the accounts table.
    - creatorId VARCHAR(255) NOT NULL, 
    > This should be set up the same way that the id is set up on the accounts table, without the primary key

    In the table, space down and then create a Foreign Key:
    - FOREIGN KEY(creatorId) REFERENCES accounts(id) ON DELETE CASCADE 
    > This is the foreign key to this table, which is the creatorId that is created in a different table, then it  REFERENCES the accounts table at a specified id. Then, if anyone deletes their account it will CASCADE and delete all of the albums associated with that account so that there isn't any orphan data in the database.

    To put that creatorId on something that is created on the table with and INSERT INTO command:
    - INSERT INTO albums (title, category, coverImg, creatorId)
      VALUES ('hot dogs', 'dogs', 'URL', 'ACCOUNTID');
    > When just testing the method in the dbSetup.sql, you can just grab one of the id's from the accounts table

    When creating the class for the album in the Controller, its prop will look like:
    - public string CreatorId {get; set;}
    > This is because in its property in the SQL database, its data type is a VARCHAR

    To pull out the user's information in order to attach it to the new data:
    - private readonly Auth0Provider _auth0Provider
      (in the same class constructor, CTRL . to create new parameters and new constructor info)

    In the HttpPost Request, make sure that the method is async and make sure that the Action Result is written like Task<ActionResult<Album>>
    - Account userInfo = await _auth0Provider.GetUserInfoAsync<Account>(HttpContext);
    > The Auth0Provider is a dependency that we need to pass in before we can use its information. Then, it will take some time to get the user info back from the auth0Provider, so we have to await it. 
    > HttpContext serves the same purpose as req and res in Node, so it basically sends in the request and its body, and the response and its body. It pulls information from the Headers, like the bearer token from Authorization.

    To ensure that only users that are authorized can use specific methods, add a decorator to the method:
    [Authorize]
    [HttpPost]
    > This Authorize will apply to the very next Http Request, and works essentially the same as the .use in Node. It throws a Forbidden error if a user attempts to use the method without being logged in.

    Before sending the info down to the Service, you can use dot notation to attach this new userInfo to the albumData:
    - albumData.CreatorId = userInfo.Id
    > This is equivalent to req.body.creatorId = req.userInfo.id in Node

    When creating the new data in the Repository level:
    - string sql = @"
      INSERT INTO (title, category, coverImg, creatorId)
      VALUES(@Title, @Category, @CoverImg, @CreatorId);
      SELECT LAST_INSERT_ID;
      ;";

      int albumId = _db.ExecuteScalar<int>(sql, albumData);

      DON'T FORGET THE RETURN

  * Next, we're going to add the creator information from the CreatorId in the table as a populate.

    We need to select and bring in two tables at once:
    - SELECT 
      alb.*,
      acc.* ,
      FROM albums alb
      JOIN accounts acc
      ON accounts.id = albums.creatorId;
    > Here we're getting all of the albums and all of the accounts and merging them together. To prevent all users from having all albums created on their account, we need to add the ON in order to add the condition where the account id is the same as the creatorId on an album. 
    > Additionally, we alias out the one album and creator with alb and acc, and then select them in the order that you want them to appear back from the database. You might want to see the account information first, or the album information first.
    > All of this together is essentially creating a virtual like in Node.

#STUB - Populating information from another table
  * To populate the information that you want in C#:

    First, create a profile class in the Account model. It should only contain the information that you want users to be able to access.

    Next, create a nested Profile class on your class in the Controller, for the thing you want to be populated:
    - public Profile Creator {get; set;}
    > Make sure that the table has this column on it as well.

    Then, create that item in the method that you want to have it populated on in the Repository. In this case, it's the Get method.
    - List<Album> albums = _db.Query<Album, Profile, Album>(
      sql,
      (album, profile) => {
        album.Creator = profile;
        return album;
      }
      ).ToList();
    > Here, in the Query we are getting back two types of data from the table. An Album and a Profile. We pass those in, and then the second Album is the one being expected as the return from the method.
    > (album, profile) are the differentiated pieces of data from those tables, the =>{} is the map function that puts the profile parameter onto the album.Creator property. Then the map function expects to return something back. The return album does that. The album and profile match the ones from the Query parameters. 
    > **NOTE PAY ATTENTION TO THE WAY YOUR WRITE YOUR SQL SELECTS. They need to match the same order that they are passed into your Query.**

#SECTION - Many to Many Relationships with C# and SQL

#STUB - Creating the table:
  1. After creating the typical properties on the table, you will add:
    FOREIGN KEY (albumId) REFERENCES albums(id) ON DELETE CASCADE;
    FOREIGN KEY (accountId) REFERENCES accounts(id) ON DELETE CASCADE;

#STUB - Creating the Model:
  1. Your model might need to inherit all of the members of a different class. In order to use inheritance for this, write your class like this:
    public class ProfileCollaboration : Profile
    {
      public int CollaborationId {get; set;}
    }
  > The : Profile brings in all of the members of the class Profile and puts them into the ProfileCollaboration class. The only thing that you need is the differing member, which in this case is the CollaborationId from the Collaborator class. This merges the two classes together more easily.

#STUB - Writing the SQL statement:
  1. The above class will be missing essential information, like the name and picture from the account. In order to grab these properties, write the SQL statement like this:
    SELECT 
    collab.*,
    acc.*
    FROM collaborators collab
    JOIN account acc ON collab.accountId = acc.id
    WHERE collab.albumId = @albumId

  > This merges together the two tables so that we can grab the properties off of them that we care about.
  > The .* is the same as dot notation, the star grabs all properties off of the item. However, we can use dot notation to grab individual properties instead.



#SECTION - Facts that will help with the Final

#STUB - Making a virtual count:
  - In the sql string in the repository:
    SELECT
    c.*,
    COUNT(cm.id) AS cultistCount,
    acc.*
    FROM cults c
    LEFT JOIN cultMembers cm ON cm.cultId = c.id
    JOIN account acc ON acc.if = c.leaderId
    GROUP BY c.id;
  > This creates the virtual count. It counts all of the id's from the cultMembers table, where the cultMember's cultId equals the cultId. The GROUP BY _should_ be making null's on the tables into 0's where there isn't a count on the specified table.
  > The LEFT JOIN will join two tables where their properties match, or where they don't it will return the count as 0 instead of ignoring the table or creating a null/creating new data so it isn't null.


#STUB - Making a Repo item:
  - In the class model:
    public abstract class RepoItem<T>
    {
      public T Id { get; set; }
      public DateTime CreatedAt { get; set; }
      public DateTime UpdatedAt { get; set; }
    }

  - In the inherited class model:
    public class CultMember : RepoItem<int> => Here the int represents the id, which will either be an int or string that the T is the placeholder for.

  > The <T> is a placeholder for whatever type will be used. In some cases, it might be a string, int, or other class model.
  > This is a class that extends members on a class that will exist on almost every class. This is like Id, CreatedAt, and UpdatedAt.
  > An abstract class is one that will never be instantiated, it only exists to support other classes.

#STUB - To ensure that only one can be made:
  - In the table, add UNIQUE(cultId, accountId)
  > This adds the constraint that the relationship between these two members can only be created once. Your account ID can only exist with this cult ID one time.

#STUB - Editing a user's account:
  - In this case, the service and repository are complete. You only need to finish the controller side. Most of it will look the same as any update, except that you will send down the user email instead of their ID.
    Account account = _accountService.Edit(accountData, userInfo.Email);



