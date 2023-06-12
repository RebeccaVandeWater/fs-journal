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

#SECTION - Facts



#SECTION - Syntax





