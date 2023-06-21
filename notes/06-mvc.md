# MVC - Model View Controller

#STUB - Shortcuts
- CTRL+p to use jump between files in the file explorer.


#SECTION - How to make an MVC file
1. In Powershell:  bcw create > Enter
2. Choose MVC for the project template
3. Use the built-in VSCode init repo instead of in Powershell, select 'no' for init repo
4. cd into new folder
5. ls to see what's in the new folder if you want.


#SECTION - To begin building out a webpage in MVC **BUILD SMALL, TEST SMALL** _Test items line by line to ensure something works and that you understand WHY_
1. Go to controllers folder
2. Make a new file, name clearly about what it will be controlling (i.e., PlayersController) (These words will be pascal-cased to show that is a class)
3. To make sure that the controller is able to be used in other parts of the code (FIRST LINE OF CODE IN FILE):
    - export class PlayersController{
        constructor(){
            console.log('Players Controller loaded')
        }
    }
    - we are EXPORTING a CLASS that we are building out. The CLASS is the CONTROLLER that is doing something. Make sure that it is properly connected with a console.log inside a CONSTRUCTOR which fires off as soon as the page loads. This should be the first step every time you build a website until you are very comfortable with MVC.
4. Go back to the router and make sure that you are calling controller: PlayersController, in an object in the router to ensure that it is connected.


#SECTION - To build out something a user can manipulate (ex: clicking a button)
1. In previous code: 
    - export class PlayersController{
        constructor(){
            console.log('Players Controller loaded')
        }

        <!-- NOTE public methods accessible to the user -->

        sayHello(){
            <!-- NOTE the method is not called with the word method or function, just with its name in a class. The file knows that its a class because of the parentheses -->
            console.log('This button works')
            console.log('Good job testing small properties of your code!')
        }
    }
2. In order to call this in the console, remember that it is nested deeply. Call with app.PlayersController.sayHello()
3. Go to index.html
4. In main, or wherever you'd like the button, create a button with the normal button tag. 
5. Hook it up with an onclick="app.PlayersController.sayHello()" 
<!-- NOTE: js is case-sensitive, make sure you are calling the controller and function exactly correctly. -->
<!-- NOTE: like previously, remember that the method is nested deeply and you need to all it from its full origin. -->


#SECTION - App State
- The place where we store all the data in MVC, like variables and arrays.

- To recognize whenever something changes in the app state, we can register a listener that watches for specific changes in the app sate. 

- In the constructor of the controller that you want changed, include:
    AppState.on('coins', _drawCoins)
    in the string of the first value is what we are watching, the second value is what you want to happen.
    in this case, whenever coins changes, it will draw coins and update the page.

    This makes it so that you don't need to have an increase and decrease function for something in the appstate. It also makes it so that you don't need a million draw functions on something.

    You can also trigger the appstate in a Service when you put the listener in the service with emit
        AppState.emit('myGachamons') => in a function that rolls different gachamons (toys) when a button is clicked


#SECTION - Building out a collection of data (these are called classes, not objects, but they serve the same purpose.)
1. Go to the Models js app
2. Create a new file that is also easy to understand (e.g. Player.js)
3. Create another class:
    export class Player{
        constructor(name, imageUrl){
            <!-- NOTE: By adding name in the parameter, this acts as a constuctor that is using name as a guide. This requires you to pass in a name, and also an img if you would like something like that. -->
            debugger
            <!-- NOTE: this allows the dev tools to read the code line by line and will stop if there is a bug. It will allow us to see what is happening line-by-line. You can take it out as soon as you have solved your problem, know what's going on, etc. It's another way to test the code instead of a console.log as well. -->
            <!-- NOTE: this is a keyword that refers to a property on the same object. -->
            this.score = 0
            <!-- NOTE: this essentially says on THIS player their SCORE is set to 0 -->
            this.name = name
            <!-- NOTE: the user will set their own name as described above -->
            this.imgUrl = imageUrl
        }
    }
4. Go back to the app state.
5. Create a variable and make it an array (make sure it is connected to the player controller, it'll be at the top of the app state if it is)
    players = [
        <!-- NOTE: to build out a new class, use the word new -->
        new Player('Jeremy')

    ]

6. To test that this works: 
    in the constructor, you can also console log the section of the app state that you want.
    console.log(AppState.players)

7. To create a new object (i.e. player)
    - new Player('Jeremy')


#SECTION - Drawing an object to the screen (this is the job of the controller!)
1. Draw a function outside of the controller method, so that it is a private method that is inaccessible to the user but can still be called by the controller. This is the encapsulation that MVC is important for.
2. When writing the function, start it with an underscore to show that it is a private method:
    function _drawPlayers('draw players works');
3. Call the function inside the constructor in the controller method. This will only run once and only when the class is substantiated. It is called syntactically the same way as we have been doing.
4. On each player class, store methods that can call a function
    get PlayerDetails(){
        <!-- NOTE Get methods must return a value, and they do not take in any parameters. However, they can print out the current values of the player class if they are contained in `` and use the this keyword -->
        let details = `Hello, my name is ${this.name} and my score is ${this.score}`

        return details
    }
5. Create the draw function that uses the app state:
    function _drawPlayers(){
        let players = AppState.players

        <!-- NOTE: test that this works with a console.log, you can drill into it the same way as before with dot notation and getters -->
    }
6. Create a template in HTML that looks the way you want it to.
7. Go back to the original model that you created
    get PlayerCardTemplate(){
        return /*html*/ (will make it look like html in js)`HTML TEMPLATE`
    }
8. Call the function in the controller draw function (_drawPlayers)
9. Go to the util files, which contain utility functions
10. Go to the Writer util files
11. Find the desired setHTML or setText function
12. Call the function in the draw function
13. Make sure to put an id on the section that you would like the draw function to be inserted in. 
14. To connect the object pieces to the template you are using, use string interpolation, making sure that the string interpolation is in the sections that those pieces would normally go. If you want a name in a p tag, you might write it like: <p>`${this.name}`</p>
15. Use concatenation to add more than one HTML template to the page.
16. To automate adding to the HTML, create a placeholder string with a for loop:
    let template = ''
    players.forEach(player => template += player.PlayerCardTemplate)
17. In the function, you can write setHTML('players', template)


#SECTION: To write and connect CSS

1. Create a class selector like normal, with the style you want.
2. Instead of using the class selector in the html like we normally would, go to the model you want to style instead.
3. Add the css class to the html class in your template.


#SECTION: To change values in js and on objects
1. Go to the services folder.
2. Create a new file that is clearly named for what it will do. Don't forget that it should only affect a like group of things!
3. Create a new class that you don't want the other files to change
    class PlayerService
4. Set up a class that can change based on the previous one which the other files can change. This is the singleton. Services do not generally have a constructor. Neither do the models that we make in the app state, these are exported separately like below. This is, again, encapsulation. 
    export const playerService = new PlayersService
5. Use the new variable on something like a button so that it is used somewhere and you can see its effect. 
    <button onclick="app.PlayersController.increasePlayerScore()">
6. Call the function underneath the constructor in the export function in the controller.
7. To call the service to use its methods, write it in the previous function and hit tab to add it.
8. To use the app state in your service function, write a new variable
    increasePlayerScore(){
        const player = AppState.players
        console.log('players:', players)
    }
9. Use string interpolation in the HTML template to pass through a player name into the method you want to change, that way their piece is specifically targeted. Make sure that the parameter is available in the method in the service. Use single quotes on the string interpolation so that it is read as a string.
10. Console log it to make sure it is passed appropriately
11. Make a find function that is set to an appropriate variable so that you are changing the correct object's piece.
12. Make another HTML template that is able to change according to the new object's piece. At this point, you will move over to the controller, and you will no longer use the service. Remember that the controller changes the view, the service changes the values that the controller draws. They have different jobs!


#SECTION: To add a form that input fields can add objects with
1. In HTML, add a form that users can input text into (go to pingPong in CodeWorks GitHub to see the specific form syntax)


#SECTION - Adding nagivation & pages to your project
- The router will call controllers AND views by injecting paths and views depending on those paths. In the "views" folder, you will be able to create a new view that has set HTML that will inject in the new view when the navigation is clicked and passed through the router.
    - While you can create a string of HMTL in your router, this can make it needlessly long. The "View" page abstracts out that job from the router to keep your code clean.

- You can put a navlink in the header of your HTML, which will add a hash reference to the end of your localhost:8080 page, which will put in the path that your router will be looking for.

- 



#SECTION - Local Storage
- When passing a parameter into the constructor of a model, be mindful of passing in one set of data (object) instead of properties separated by commas. This will allow you to pull informatin from local storage easily.

- This has been written in MVC for us in Store.js. If we call (NOT CHANGE) this template, we can save and load something in our local storage

- We can put the save/load functions in the Service with a private service
    function _saveMyGachamons(){
        saveState('mygachamons', AppState.myGachamons)
    }

    - NEXT call the function after something might be pushed into an array that you want to save, in that function in export.

    - THEN in the appState, you will want to load values so that the things that you want to save are called as soon as the page loads.
        myGachamons = loadState('myGachamons', [Gachamon])
        This uses the key of myGachamons, and then tells you what kind of data type this is (an object in an array)

    - LAST load the appState data in the controller so that when you refresh, it already appears.


#SECTION - MVC Functions

- **Import/Export** helps connect files together while also preventing the user from getting into the files of an app and messing around with them. You cannot export something without importing it somewhere else. **Encapsulation**
    - To use export: export const VARIABLE1 = 'STRING'
    - To use import: let VARIABLE2 = VARIABLE1
    - Intellicense will know where the variable is coming from and what it is called. It will auto complete for you and if you hover over it, you will be able to see where it's coming from.
        - Avoid writing it with file pathing (like using ls in the console), setting and pulling variables is less easy to screw up.
    - You can also export functions: 
        - export function sayHello(){
          console.log('hello world')
          }
        - to import: let helloFunction = sayHello()

- **ObservableAppState** is where most of our global variables will be. It is where our data should be stored. This is also more encapsulation that helps our app work without user interferance. 


#SECTION - Classes

- Big, fancy objects with great intellicense. You can store variables and functions in a class and then export them out to another file.

- Classes allow for encapsulation via bundelling a lot of like code together, making it easier to use.


#SECTION - Facts

- Models are classes, view is what the users see, controller only allows users to see what we want them to. Controllers are basically the only thing that can change the models.
    - It may feel redundant to have a controller, service, and app state, but this allows your code to be secure from users.

- There will likely be different services and controllers for each data type.

- The bcw mvc file has a ton of files already set into them! This is typical no matter what company you go into. They will typically have pre-prepared folders/files for you to build in. In the bcw files, some you will never need to go into.
    - there is an index.html file with link tags. Bootstrap and style.css have already been linked.
    - script tags for javascript, sweetalerts, and other script sources have already been linked.
        - type: module on a js tag means that your js files are broken into smaller files that you will be able to use import and export on.
        - **You NEVER have to go back into app.js and change anything.** You don't need to know what's in there either. _HOWEVER, you will need to learn about classes, building classes, and the key words that affect them._
    - js is able to inject inner.HTML here as well.
    - A lot of the pre-made mvc code is made as a reference for us to go back to later to see how it works.
    - AppState.js will be used by us frequently

- All methods are functions but not all functions are methods.

- Controller will call on the html after the event is complete to change the view. It cannot change the app state, that is the job of the Service.
    - Controllers are registered in the router
    - Routers are another version of an array
    - You can call a controller using a path in the router on the controller object.
    - a constructor is the same as calling a function at the bottom of our js sheet. This allows something to run as soon as the page is loaded.

- import (Pop) is the built in sweet alert

- You only use new to create a new class object

- Getters don't need to be invoked because they automatically return something ( make sure you write RETURN in them!)

<!-- NOTE: --> Generating ID's
- There is a utility function for generating id's that you can bring in on your model.
    this.id = generateId()

    That way, when you are using a find function you can grab something by its unique identifier so that you can find specific items in your AppState array.

<!-- NOTE: --> Generating Dates
- You can create dates and times in your objects by using the date function
    this.listingDate = new Date()

    You can also supply arguments so that it has the specific date/time that you want it to.