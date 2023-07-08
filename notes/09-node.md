# Node

#SECTION - Getting Started
1. In the controller, type in bcw create > node-server

#SECTION - The tour of node
- In the client folder, you will see your index.html folder
- You will see an env file with environment variables that will be familiar due to the MVC pattern.
- In the server, you will see main.js. It is relatively small. You might need to comment out the DbContext.connect line of code. You will not need to interact with it much, it just adds middleware.
- The ConfigureGlobalMiddleware statif function is meant to be what the user might interact with throughout the application. It makes information available to git, localhost, etc 
    - helmet is a line of code that is meant to take out malicious or incorrect code. 
    - bp.json means that all parts of the body are JSON code.
- Controllers and services are still present like in the MVC design pattern.
- You will also have a Startup.js file which creates hallways for the router, which connect all controllers (doors in the hallway) to the router

#SECTION - Controllers in Node
- The BaseController registers your other controllers so that they can be sent in the hallway to the router
- The ValuesController is an extension of the BaseController which allows controllers to be connected more easily.
- They will typically be the first thing that you set up when you make your server.

#SECTION - Postman


#SECTION - MongoDB
- This is a database which holds and handles all of our data.
- You need to make a free account in order to use it.
- For this purpose, you can make your Project Name CodeWorks Classroom.
- A cluster is the collection of your databases.
- When you add a new Database User, don't make your username and password the same as what it is for the overhead account.
- You need to add the IP address of your location that the database will be used in. It's easier to select "Allow Access from Anywhere" instead of adding your IP address every time you move your computer to a new location.
- When you connect, you will need to copy and paste the connection string with the correct password into the .env file with the connection string inside it, without quotes.

#SECTION - Models/Schemas
- ORM: Object Relational Mapper; Mongoose is the ORM for our node model
- Schemas have almost the exact same purpose as models
- 

#SECTION - Facts

