# Application Architecture, MVC Design Pattern
01. What are the Pillars of Object Oriented Programming (`OOP`)?
  
  > Abstraction: Abstraction means to create code that is generic and reusable. This allows you to streamline your code, making errors easier to find, your code easier to use in a team setting, and easier for the user to interact with.

  > Encapsulation: Encapulation is separating code into different modules, functions, and variables. The purpose of this is to not only clean up your code so that it isn't "spaghetti", but also to hide it away from users. The users will be able to see the results of encapulated code, but won't be able to manipulate it maliciously or accidentally. And again, it's great to prevent errors as the errors either won't occur as often with separated and cleaned code, and they will be easier to find.

  > Inheritance: Inheritance is when your code is transferred from parent to child, and not the other way around. This is Liskov's Substitution from the SOLID principals in action. It allows your code to be appropriately transferred into or separated from each other so that it doesn't break. If you encapsulate and abstract correctly, then this should also effectively help clean up your code.

  > Polymorphism: Polymorphism is when you are able to effectively use parents to code child behaviors. This is where you can replace generic code you have previously made and tested with code that you may need.


02. How does `export` differ from `export default`?
  
  > You can use export when you need to move multiple values between modules. If you only need to move over a primitive value, or just a single value, you can use export default instead. They both allow for different ways to organize your code.

03. What is Encapsulation?
  
  > Encapsulation is the storing and separation of data and functions from other files. This helps when you change values that functions might be dependent on. Encapsulation allows you to change the values without breaking your code. 

04. What are some of the benefits of the `Proxy` object that we are using in our structure for applications?
  
  > A Proxy is able to watch for changes on an object, and then do something based on that change. This is helpful because it allows us to refactor our code and more easily access/change objects depending on conditions that we set.

05. What the difference between a `class` and an instance of a `class`?
  
  > A class is a model for an object that you might be able to create. An instance of a class is a specific item that you have created of that object, typically made in the AppState. 

06. What is a computed Property?
  
  > A computed property is a property on an object that you can create using class values. If I have a player that has a name and a score, I can pass in (with other work) a form that the player completes with their name and earned score. Then, I can put that information into a model that pulls down that information and draws it into the screen so that we can see it. This information is typically returned with a getter.

07. What is the purpose of the `MVC` pattern?
  
  > The MVC pattern helps add organization in your application. It keeps the objects separated, but still accessible by, the functions which control the user's experience.

08. What is the job of the `Controller` in the `MVC` Pattern?
  
  > The controller handles user input and changes the user's view depending on their interaction in the Model. It literally controls what is on the page.

09. What is the job of the `Service` in `MVC`?
  
  > The service operates and changes data out on our models that are stored in the app state. This is the only thing that can change the AppState (without breaking the MVC pattern). 

10. What is the job of the `Model` in `MVC`?
  
  > The Model is a subsection of the AppState. It stores the classes that the AppState then creates and saves instances of.