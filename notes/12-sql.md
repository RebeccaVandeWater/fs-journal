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