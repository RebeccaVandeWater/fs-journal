# Intro to Server side concerns with JavaScript
01. What do the letters of the acronym `CRUD` stand for?

  > C - Create, this is the POST request.
  > R - Read, this is the GET request.
  > U - Update, this is the PUT request.
  > D - Delete, this is the DELETE request.

02. Each action that `CRUD` represents maps to an HTTP request. What HTTP request does each `CRUD` action correspond to?

  > As stated in question 01: C corresponds to the POST HTTP request, R corresponds to the GET HTTP request, U corresponds to the PUT HTTP request, and D corresponds to the DELETE HTTP request.

03. What does `ORM` stand for? Which `ORM` do we use when interacting with MongoDB

  > Object Relational Model: We use Mongoose to take the information stored in MongoDB and translates it into Javascript that we can use in VSCode.

04. Which two `HTTP` request types include a body?

  > POST and PUT require a body. POST creates a brand new object with the user-provided data. PUT updates an already-existing object with user-created data.

05. In a/an _______ coding model, when you call a function, it returns only when the action has finished and stops your program for the time the action takes. Likewise in a/an _______ coding model, multiple things are allowed to happen at one time. When you perform an action, your program continues to run.  Fill in the blanks.

  > Asynchronous
  > Synchronous

06. What are the three types of data relationships? Provide an example of each.

  > 1:1 - In this case, only one object can be related to only one object (and vice versa). An example would be that a user will only have one phone, and the phone would also have only one user.
  > 1:N - In a One to Many relationship, one object might be related to many things, but those many things only belong to that .one object. An example would be that a driver might have many cars, but those cars are in the possession of only one driver.
  > N:M - In a Many to Many relationship, a group of objects might be related to another group of objects. An example would be that a planet might have many species and those species might also live on many planets.

07. What is middleware?

  > Middleware is software that handles information between different applications. It helps speed up the coding process, as well as the user's interaction with a developer's website. Mongoose, which is also an ORM, is middleware between the developer and MongoDB.

08. The ______ pipeline delivers information from the client while the ______ pipeline returns it. Fill in the blanks. 

  > Request
  > Response

09. Demonstrate the pattern that is used to include a request query with the client's `HTTP` request providing the property `tag` and the value `winter`.

  > ?tag=winter
  > Here, the query is indicated with the ?. Then, it is followed with the key/value (or property/value) pair tag=winter. The entire query would be appended onto an /api url.

10. What is a ***virtual property***?

  > A virtual is a model that is added to another model via a function in that secondary model. For example, we might want to assign authors to books when we pull up an active book on a website. In this way, we can see the author model's properties (like their name) from the server, while accessing a book model in the client.
