# JavaScript


#SECTION - Getting Started
1. Set up your project as normal with:
    - style.css
    - index.html
    - (NEW) app.js

2. Connect your css and js to html:
    - link > css in head as normal
    - AT THE BOTTOM OF YOUR BODY script:src > app.js

#SECTION - Variables & Strings

- To make one variable:
    - let VARNAME = VALUE/ARGUMENT;

- To call (not declar) a variable to change it:
    VARNAME = CHANGE (note: declaration like let is not used)

- To create a group of variables (such as on colors) - 
    root:{
    --COLORNAME: #HEXCODE;
    --COLORNAME: #HEXCODE;
    }

    - Now you can insert the variables into something like a CSS selector if you wish. This makes it much easier to type out and setting out themes that you can change quickly. 
    - It isn't recommended to use it if you're only going to use it once, as it would be redundant. 

- To combine variables:
    - let VAR1 = ARGUMENT
    - let VAR2 = NEW-ARGUMENT
    - let VAR3 = VAR1 + VAR2
        - To put a space:
        - let VAR3 = VAR1 + ' ' + VAR2

- If you are using quotes or double quotes in a string, make sure that you are using the other one for apostrophes or quoting people.
    - EXAMPLE:
        - let STRINGWITHQUOTES = "Isn't this cool."
        - let STRINGWITHDOUBLEQUOTES = '"I'm really smart" said Savannah'

- STRING INTERPOLATION:
    - takes data from js and puts it into a string
    - EXAMPLE:
        - console.log(`This is the full VAR: ${VAR3}`);
    - NOTE: back tics `` must be used in order to call string interpolation

- A BLOCK is any chunk of code that lives in the curly braces {}
    - LET is defines variables that are block scoped. 
    - LET can be redefined inside functions without changing it globally, therefore it is easier to avoid errors using let.

- If you get REFERENCE ERROR in regards to your code, it is likely not defined correctly or is not in the right scope

- VAR is a way to declare variables, but is either globally or functionally scoped depending on where you put it. It is easier to get errors this way depending on when, where, and how you define it. Some definitions that you set can override other definitions.

- CONST is a way to declare variables that is block scoped like let, but it is a CONSTANT variable, and does not change.
    - You can, however, make it more specific with dot notation
        - NON-EXAMPLE:
            const greeting{
                console.log("Say Hi);
            }
            const greeting{
                console.log("Say Hello instead");
            }
            **WILL NOT WORK**
        - EXAMPLE (making it an array, not a variable):
            const greeting{
                message: "Say Hi";
                times: 4
            }
            greeting.message //Say Hi
            OR
            greeting.message = "Say Hello instead";
            **WILL WORK** as it changes the section of the array that was previously set.

#SECTION - Booleans

- To declare a boolean:
    - EXAMPLE:
        let VAR1 = true
    - To change it:
        VAR1 = false (note: again, let is not used)

- IF statements automatically run to determine if something is true, unless it is given an argument otherwise.
    - ELSE statements will then automatically run if something is false, if you write the else statement.

#SECTION - Numbers
- EXAMPLE:
    - let NUMBER = 3

- NUMBER++ is an INCREMENTOR (adds 1)
- NUMBER-- is a DECREMENTOR (subtracts 1)

- To change the value: 
    - NUMBER += 1 (adds 1 and stores the new value in the variable)
    - NUMBER +1 (doesn't change the value of NUMBER)
    - A longer way of doing it: 
        - NUMBER = NUMBER + 1

- Javascript uses PEMDAS, so make sure you write your longer operations correctly in order to get the correct answer
    - let COMPLICATEDNUMBER = (4+4) * (75/5)
        - the Parentheses will be solved first
        - the Multiplication symbol will be solved next

#SECTION - Objects 
- A way to store multiple pieces of data inside one piece of data

- OBJECT:
    let OBJECT = {
        NAME: 'STRING',
        AGE: NUMBER
    }
    - **USE CURLY BRACES**

- Objects are made of KEY VALUE PAIRS 
    - name: 'string' > name is the KEY, 'string' is the VALUE

- Keep in mind that when you make an object, the key value pairs that you put inside it are only in scope on that object. You can't create a property outside it and expect it to be in the object.

- You pull properties out of an object with DOT NOTATION:
    - EXAMPLE: 
        console.log(OBJECT.NAME) //'STRING'

- Order inside objects isn't read from the top down, they only keep track of objects that have key value pairs.

- Objects can be nested:
    let let OBJECT = {
        NAME: 'STRING',
        AGE: NUMBER
        OBJECT2: {
            NAME2: 'STRING',
            AGE2: NUMBER2
        }
    }

- If you set an objects property equal to another variable's property, and then change what that property is equal to, you will also change the objects property. This is because it is a reference object, not a primitive object. It does not make a copy of the object, it makes a REFERENCE to the one already in memory.

#SECTION - Arrays
- When dot notating into an array, don't forget to write where you want to be in an index with [indexNUMBER]

- These are ways of showing collections of data. 

- To call a function every time the page loads, call the function at the bottom of your js page (or after the function) 
    - EXAMPLE: randomNumber()

- let breakfastItems = [
    'apple',
    'bagel',
    'nothing',
    'rice krispies'
]
 - **USE SQUARE BRACKETS**

 #NOTE - Draw something from an array to the screen
 1. Give the place where you want it to be in the html an id
 2. Create a function for the element to draw
    - let drawElement = document.getElementById('elementId') > will be necessary for this to work
    - drawElement.innerText = arrayString (like an emoji or picture, variable is in forEach loop below)
 3. Create a forEach loop with an empty string outside of it that the properties can save to. The string should be inside the draw function that the forEach loop is inside.
    - let arrayString = ''
    - array.forEach(array => {
      arrayString += arrayEmoji
      })

 #NOTE - Random Number Generator

- To make a number generator: 
    - in a function, write something like: 
    EXAMPLE: let randomNumber = Math.random() 
             console.log('random', randomNumber);
    - To make the number a whole number, write it like: 
    EXAMPLE: let randomNumber **Math.floor(Math.random() * NUMBER OR ARRAY.LENGTH)**
             console.log('random', randomNumber);
    - Math.floor rounds down, Math.ceiling rounds up
    - You can also make the randomizer on an index of an array by using randomIndex = array[randomNumber]
    - You can target a random item in an array and change one of its properties with:
    EXAMPLE: randomIndex.property = true

 #REVIEW - Check Week2 > Day2 for array method practice

 - If you want to use mixed data types inside your array, just use an object instead. Arrays are better used when they have the same data type (strings, numbers, objects, etc.)
    - for loops would get really complicated if you use different data types. Your code should be predictable.

- The length of an array will always be one more than the index.

#NOTE - Array Methods

- **.find** will find an object in an array for us
    - EXAMPLE: let foundCat = cats.find (cat => cat.name == 'Gopher')
    - Once find meets the condition you set, it will stop running. It will only find the first thing that meets this condition. So, only try to find a unique property (such as a name or id) on the array because otherwise you may not get all of the information that you want.
    - If you do not give it a property to find, it will read it as a conditional and find something that is true on that property. EXAMPLE: cats.find (cat => cat.hasTail) is read as a conditional, and will return the first item where hasTail = true. 

- **.filter** 
    - Creates a brand new array where the filtered conditional is true
    - EXAMPLE: let filteredCats = cats.filter(cat => cat.hasTail == true)
        - The new array is filteredCats, and it only has cats that have hasTail = true in their array.
    - It does not delete the previous array, it just copies it with the array items that have the conditional true.

- **.sort** 
    - EXAMPLE: let sortedCats = cats.sort((cat1, cat2) => cat1.age - cat2.age)
    - Compares each thing in the array to other things in the array. If something previously met the conditional of the sort, it'll compare it to the new items as well.
    - You can use - to have the sort in ascending order, or + to have it in descending order.
    - Less useful than filter and find

- **.map** 
	- Changes all the properties on the arrays that meet the condition. 
	- Does not change the original array.
		- EXAMPLE: let numbers = [1, 2, 3, 4]
							 let changedNumbers = numbers.map(number => number *2)
							 console.log('changed', changedNumbers);

#SECTION - For Loops

- for (let i = 0; i < 1; i += 3)
        i is the initializer
        i < 1 runs the code as long as it is true (the conditional)
        i += 3 is the speed in which we are iterating through the array (incrementor)

- an ALIAS references each thing in the array, ex. let cat = cats[i]
- _Be careful_ when using <= for your condition, you should be careful because it will continue to run through the length of the array, as the length may be 3 while the index is 2. So, the length will try to access something at 3 that doesn't exist.
- The length of an array will always be one more than the index.

- Use && to include two conditionals in the loop.

#NOTE - forEach

- Syntax:
    ARRAY.forEach(cat => console.log('😻', cat))
    1. Alias out what you want from the function (cat => )
    2. Give it something to do


#SECTION - Functions
- To declare a function:
    function sayHello(){
        console.log("Hello World")
    }

- Sometimes when you call a function and it doesn't return anything, like something new, it will return "undefined" at the end of your function. That's normal and doesn't hurt anything. You can tell it to return something at the end to fix that, such as return 1. 

- You INVOKE functions with parentheses
    - EXAMPLE: sayHello ()

- To save data from user input, store it inside a variable or array. Set them as an empty string or something similar to ensure that there is space inside it.
    - EXAMPLE: let userInput = ' '
    function sayHello (){
        userInput += 2
        console.log('This is the userInput', userInput)
    } _it should log +2 every time the specified userInput is used (like clicking a button, note that it does need to be connected to html with a running function for this to work properly).

- If you're writing the same functions over and over again, make one function that does those repeated things. Definitely practice making multiple functions and making sure that they work first, then you can work on abstracting your code.

#NOTE - Parameters and Arguments:

- A parameter is what runs through the function that a user provides.

- An argument is a value, which typically goes into the parameter. 

- A parameter is manipulated by the argument (ex: the thing printed to the console).

- function selectNumber(number){
    userInput += number
}

- This parameter can be provided in the html
    onclick = selectnumber(1)

#NOTE - Running Functions

- **onclick** in html you will write the run argument with the function's name inside it.
    - EXAMPLE:
        onclick = "sayHello()"

- Put id's on things in html that you want to interact with your javascript. Do not put two id's that have the same value
    - "document" references things in the html
    - let givenElement = document.getElementById('idInHtml')
    - you can change the innertext (something that is typed inside the element) by using .innertext on the thing that you want to change, and making it = to a new value (such as a flexible variable that changes with user input)
        - givenElement.innerText = userInput



#SECTION - Facts
- NULL is a datatype without a value, it is typically used to save a variable that will have data put into it later with back-end functions
    - Example:
        let nothing = null

- Undefined means that something is not properly defined and doesn't have a value. **NULL** is a value!!

- You can group console logs with console.group('name'), and end it by putting console.groupend() at the end of that group.

- **pseudocode**
    - Writing out function goals in plain English before creating the actual functions for it.
    - EXAMPLE: // get a console log of the avocado emoji, store an avocado emoji somewhere, console log the emoji stored within js


#SECTION - Syntax

- Camel Case:
    - In javascript, use Camel Case in order to denote variables that have more than one word. Capitalize each word after the first
    - EXAMPLE: newString

**Don't Use in js**

- Snake Case:
    - new_string

- Kabob Case: 
    - new-string





