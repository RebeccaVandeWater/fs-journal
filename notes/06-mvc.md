# MVC - Model View Controller

#SECTION - How to make an MVC file
1. In Powershell:  bcw create > Enter
2. Choose MVC for the project template
3. Use the built-in VSCode init repo instead of in Powershell, select 'no' for init repo
4. cd into new folder
5. ls to see what's in the new folder if you want.


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

