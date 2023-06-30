# Understanding Asynchronous Code, and API's
01. What is the difference between `asynchronous` code and `synchronous` code?

  > Synchronous code is code that runs top to bottom in order like we write it. However, if we have code (like getting something from an API) that takes just a little bit longer, or if we have a code that needs to run after a user responds to a prompts, then we will want to use asynchronous code. In this case, we can write it "synchronously" but take advantage of async and await in order to make JavaScript stop applicable code from running until a promise has been fulfilled (a response from an API, a user click, etc).

02. What is an event listener?

  > An event listener is a method that, when given a piece of code like a variable, alerts the function it is placed in when the code it is "watching" changes. This allows a function that the listener is placed in to run. It's sort of like a promise that is waiting for a response.

03. What does *REST* stand for, and in simple terms what does it mean??

  > REpresentational State Transfer. This means that the user will request information from a server, which will then return the information in its current state, with all of its applicable details. The request will involve one of the CRUD methods in some form.

04. What is a callback / higher order function?

  > A callback or higher order function is a function that is able to handle more generalized functions via asynchronous code. They are able to let the browser wait for code to finish running, without stopping the website completely. They are also able to handle hidden-away code that has been encapsulated for the sake of writing code that is easier to read and find errors in. Hoisting plays a big part in this process, as well.

05. What is a `promise`? How do you capture an error from a `promise`?

  > A promise is a set of code that is waiting for a response from another function or the user. It will wait (pend), and then the promise fill be fulfilled (resolved), or will fail (be rejected). It can solve the Callback Hell problem of having multiple functions nested inside each other that are waiting for the previous function to resolve before running. Instead, the promise can be chained to a callback in order to resolve a function more quickly. Promises and callbacks can be written with try/catch methods that allow the promise to either be resolved, or stopped and logged as an error quickly if rejected.

06. Name three processes used to make requests over `HTTP`?

  > GET, PUT, and POST are the three processes which make requests over HTTP. These use an API in order to make a request for information that can be listed, created, or editted. Then, if the request was written correctly, these requests will be returned to the user via the API from the server's data.

07. What does the `API` acronym stand for?

  > Application Programming Interface. This allows one computer to interact with another computer via a database/server. The user requests from the first computer are intentionally limited to protect sensitive information that is stored on the server.

08. What must you do in order to `await` a promise inside of a function?

  > In order to await the promise, you have to declare the function as async before you write it, or the applicable awaiting code. This lets JavaScript know that a promise has been made, and it has to wait to move on inside that area until the promise has been fulfilled or rejected.

09. What is the purpose of encapsulation in programming?

  > Encapsulation helps keep code separated and easy to read. It also helps you find errors more quickly.

10. What is `HTTP` response code for a successful request?

  > The HTTP code 200 OK is a successful request. It means that your request went through and returned successfully.

11. What is a 400 error?

  > A bad request pertaining to information that a user requested that isn't present on the server. 
