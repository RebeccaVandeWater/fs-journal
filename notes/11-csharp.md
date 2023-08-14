# CSharp

#STUB - C# Basics

#SECTION - Getting Started

1. 'dotnet new console' in the command line of the folder you would like to be in, it will then create three files automatically for you.

2. 'dotnet run' in the console will run your C# functions so that you can test it without opening a localhost

#SECTION - Syntax
- Console.WriteLine("Hello World"); > This is essentially a console log, written differently

- _C# DOES NOT USE LET, VAR, OR CONST_ it defines variables with their types

- string name = "Jeremy"; > The type of the variable is first, then its name, and then after the value has been defined the line ends with a ; so that C# knows to run.

- char middleInitial = 'B'; > One character must be defined as char, as it is a type character

- bool jeremyLikesCats = true; > Type boolean

if(jeremyLikesCats)
{
  Console.WriteLine("Of course this is true");
}
  NOTE The curlies start on a new line from the if statement in C#

- _C# does not have truthy falsie statements!!_ You need to write if statements with a boolean or with something that will result in a boolean
  EXAMPLES
  if(firstname == "Sam")
  {
    Console.WriteLine("My name is Sam");
  }

  if(total > 2)
  {
    Console.WriteLine("The total was greater than 2");
  }

  **=== DOES NOT exist in C#** It either is the thing or it isnt with ==, however the ! operator does still exist.

- int num = 3; > int is how you define an integer (whole number)

- double halfnum = 2.5; > double is how you write a decimal, you will get an error if you try to use int on a decimal.

#TODO - Read the documentation on C# numbers, there are a lot and you should be particular about which types you are using so that you aren't throwing errors and so that you are not using up memory unnecessarily!

- To string interpolate in C#, you will write like this:
  - Console.WriteLine($"Hello, my full name is {firstName} {middleInitial} {lastName}")
    NOTE: The $ for the string interpolation is on the outside of the quotes, while the items that you would like to interpolate will be in {} inside the quotes

- To create an array:
  int[] numbers = { 1, 2, 3, 4, 5 };

  NOTE Your methods will still exist for the most part, however here are some changes:
  FOR LOOP:
    for(int i = 0; i < numbers.length; i++)
    {
      int number = numbers[i];
      Console.WriteLine(number)
    }

  _Arrays suck in C#! Use lists instead_

- List<string> names = new List<string>();

  This is an empty List with the type string and the variable name names. Then when we define the values, we create a new class with the new keyword. Note that you cannot store things inside it that aren't strings, because that's what we said it would store.

  To add something new to the list, we use:
  names.Add("Sam");
  names.Add("Savannah");
  names.Add(firstName); > This is a variable that we defined above
  names.Add("Stinky");
  names.Remove("Stinky");

  This is very similar to array.push()

  foreach(string name in names) > This pulls out each string in the collection, defines it as a name, and points to the collection names to look in for these items. This is very similar to props in Vue.
  {
    Console.WriteLine($"My name is {name}");
  }


#SECTION - Facts
- C# is strictly type-based, which means that when you declare a variable you MUST define what type of variable it is (int, string, object, etc.)

- C# will also immediately stop as soon as there is an error, it has very good intellicense and will let you know before the application loads that something went wrong. Javascript will run the application until something goes wrong.

- Whenever you write code and your line ends, you must end it with a semicolon. This is the terminator that tells C# when a line is done being written and can be run.

- Only variables that you declare should be camelCased where the first letter is lowercase. Everything else should be PascalCased where all first letters of words are uppercased.

#STUB - Building an API with C#

#SECTION - Getting Started

1. bcw create dotnet-auth

2. Set up your model with: rightclick > New C# > Class > name your class
    - C# will set up some items for you already in order to make your file ready to go! If not, make sure it has:
    namespace filename.Models;
    public class Cat
    {

    }

3. Create your model
    public class Cat{

      public string Name { get; set; } > Use the code snippet prop to get the properties that should go on your model. The properties should be PascalCased

      public int Age { get; set; } > get/set tells the code whether you can get the property and/or set the property. The getter functions can also be customized. You can use either get or set as well, like if you are privatizing a class then you should use only get, not set.

      public bool HasTail { get; set; }

      public double NumberOfLegs { get; set; }

      public Cat(string name, int age, bool hasTail, double numberOfLegs) > This is the constructor, it should share the same name as your model and should come after you have defined the properties for your model. There isn't an easy way to create and use objects in C#, so you need to pass in the properties as arguments, which should be camelCased. This serves the same purpose as passing through "data" in the constructor
      {
        Name = name; > You don't need to use this. as long as you have defined the property that you are attempting to define
        Age = age;
        HasTail = hasTail;
        NumberOfLegs = numberOfLegs
      }
    }

4. Set up your controller with new C# > API Controller > name it
    This will also create some starter information for you in the controller to get started with

    [ApiController] > This is the type of controller that it is
    [Route("api/[controller]")] > This is the mounting path, just like the super() in Node. The [controller] grabs the public class name and uses that as the mount path. So, you don't need to rewrite that controller name.
    public class CatsController : ControllerBase > This is inheritance, like when we use extends in Node.

5. Create your first method inside your controller
    public class CatsController: ControllerBase
    {

      [HttpGet] > This defines the CRUD method that the VERY NEXT method will be doing

      public string Test()
      {


        return "Test worked"; > C# expects methods to return a value of the type defined at the start of the method (in this case, a string)
      }

      public void Something(){
        Since this is type void, nothing is expected to be returned
      }
    }

6. Set up a constructor inside of your Controller so that you can set up the matching service as a dependency
    Above your code and inside of the Controller:

    private readonly CatsService _catsService; > This keeps the service as a Singleton that cannot be changed. Readonly is = to const. Private variables are denoted with _. It's not necessary but is industry standard.

    public CatsController(CatsService catsService) > This is the constructor that creates the public-facing service Singleton
    {
      _catsService = catsService;
    }

6. Spin up your server so that you can host locally, it will automatically spin it up to localhost:7045 (this is also where you'll test in Postman)
    - This will typically give you an error because you don't have an https certificate, go to Advanced and continue to website
    - If you want to test your endpoint, type it in the URL to see the information. You can also use Swagger temporarily while we aren't using Auth by either clicking the link to the swagger docs on the page, or by typing /swagger in the URL.

7. Set up your Service for your model\
  - New C# Class
  - public class CatsService
    {
      
    }

8. Set up your repository
  - New C# Class, name your repository
  - public class CatsRepository
    {

    }

9. Go to Startup.cs and build out your Repository and Service
  - services.AddScoped<CatsRepository>();
  - _While using the fake db use => services.AddSingleton<CatsRepository>();_
  - services.AddScoped<CatsService>();

  This builds out the services and repositories that will give our controllers the dependencies that they need to run.

#SECTION - Making CRUD methods in C#

- In the Controller:
  [HttpGet]

  public ActionResult<List<Cat>> GetCats() We are expecting to return a list that has the type (model/class) Cat
    NOTE: ActionResult allows us to get HTTP responses back from our API. If we didn't have that, we wouldn't be able to get a 200, 400, etc. response from the API.

  {
    try
    {
      List<Cat> cats = _catsService.GetCats();

      return Ok(); This wraps the response in a 200 OK
    }
    catch(Exception e) > This is the error handling for C#
    {
      return BadRequest(e.message); > This is the equivalent of "next" in Node
    }
  }

- In the Service: 

  private readonly CatsRepository _catsRepository;

  public CatsService(CatsService catsService)
  {
    _catsService = catsService;
  }

  internal List<Cat> GetCats()
  {
    List<Cat> cats = catsRepository.GetCats()

    return cats
  }

- In the Repository (Talks to the database):
  public class CatsRepository > **This will work as our database this time, but will change when we use SQL!**
  {
    private List<Cat> dbCats;

    public CatsRepository() This is the constructor for the repository. **It acts as our fake database for right now. We will be using SQL later!**
    {
      dbCats = new List<Cat>();
      dbCats.Add(new Cat("Gopher", 2, true, 4));
      dbCats.Add(new Cat("Mustang", 1, true, 4));
      dbCats.Add(new Cat("Georgie", 5, true, 4));
      dbCats.Add(new Cat("Dudley", 2, true, 3.5));
    }

    internal List<Cat> GetCats()
    {
      return dbCats;
    }
  }

#SECTION - Get One Method

- In the Controller:

  [HttpGet("{name}")] the parantheses after the Get are how we define a parameter for the get method.

  public ActionResult<Cat> GetCatByName(string catName) > We are expecting a string from the HTTP request, so that needs to be defined
  {
    try
    {
      Cat cat = _catsService.GetCatByName(catName);
      return Ok(cat);
    }
    catch(Exception e)
    {
      return BadRequest(e.message)
    }
  }

- In the Service:
  internal Cat GetCatByName(string catName)
  {
    Cat cat = catRepository.GetCatByName(catName)

    if(cat == null){
      throw new Exception($"No cat with the naem of {catName}"); > Exception is essentially "error" here
    }

    return cat
  }

- In the repository:
  internal Cat GetCatByName(string catName)
  {
    Cat foundCat = dbCats.Find(cat => cat.Name.toLower() == catName.toLower); > This will allow the strings to be the same casing so that you always get the right item returned back, even if someone forgot to uppercase a certain character

    return foundCat
  }

#SECTION - Post Method

- In the Controller:
  [HttpPost]
  public ActionResult<Cat> CreateCat([FromBody] Cat catData) > This says we are getting data from the body that should be a Cat, and the variable name is catData
  {
    try
    {
      Cat cat = _catsService.CreateCat();
      return Ok(cat);
    }
    catch(Exception e)
    {
      return BadRequest(e.message);
    }
  }

- In the Service:
  internal Cat CreateCat(Cat catData)
  {
    Cat cat = _catsRepository.CreateCat(catData);
    return cat;
  }

- In the Repository:
  internal Cat CreateCat(Cat catData)
  {
    dbCats.Add(catData); > new Cat is not necessary because we cast it into the object already, in the parameters of the method
    return catData
  }

#SECTION - Delete Method

-In the Controller
  [HttpDelete("{catName}")]

  public ActionResult<string> RemoveCat(string catName)
  {
    try
    {
      Cat cat = _catsService.RemoveCat(catName);
      return Ok($"{cat.Name} has been sent to the farm!");
    }
    catch(Exception e)
    {
      return BadRequest(e.message);
    }
  }

- In the Service:
  internal Cat RemoveCat(string catName)
  {
    Cat cat = _catsRepository.RemoveCat(catName);
    return cat;
  }

- In the Repository:
  internal Cat RemoveCat(string catName)
  {
    Cat catToBeSentToTheFarm = GetCatByName(catName);
    dbCats.Remove(catToBeSentToTheFarm);
    return catToBeSentToTheFarm;
  }


#SECTION - What's in the folder?
- Startup has the Auth provider information and functions

- "public" is a keyword that allows classes to be accessible to other files when the file it is in is exported

- "namespace" is a keyword that exports and imports the file that it calls. This has the same functionality of export in Javascript. It is not the same as a Singleton!

- "using" is a keyword that imports the file that it calls.

- The Globals files make it so that you don't have to keep importing namespaces, there are files in there that allow you to call other files' code more easily.
