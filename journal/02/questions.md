# Intro to JavaScript
01. Which keywords are used to declare a variable in JavaScript?

    > We can use the keywords 'var', 'let', and 'const'. Let is preferred as it has fewer issues with scoping and can be redefined later. Const has the same kind of scoping as let, but cannot be redefined unless it is written like an array. Var is an older version that could have been functionally or globally scoped, and it was easy to get errors as a result. 

02. What is the definition of a function?

    > A function is a sub-program. It gives your code 'function'-ality. It has to be invoked with return in order for it to work, however it can be "anonymous" and not named.

03. What are the `SOLID` principles?

    > S - Single Responsibility: Every class/function should only do one job and it should do it very well. This helps with debugging. If something goes wrong, you'll notice it a lot sooner. If you need to change something, it will be much easier to find.
    > O - Open/Closed Principal: Code is open for extension and closed for modification. It should be solid enough that you can extend on it easily without breaking it. This is especially helpful when doing coding in a team/company setting where your code is changing much more often and your team might need to build on your code.
    > L - Liskov's Substitution: A child in a function should be able to easily swap with its parent without causing errors, although the parent won't be able to take on the child's responsibility.
    > I - Interface Segregation: This is sort of the same as single responsibility. However, instead of classes taking on a single responsibility, the user interface does. This has the same benefits as single responsibility on classes.
    > D - Dependency Inversion: High level classes and modules shouldn't be closely dependent on low-level ones. The code that you write should be easily replaceable so that it isn't easily breakable. 

04. Given this array: How could you remove the `pineapple`?

    ```js
    let fruit = ['apple', 'banana', 'pineapple', 'orange', 'strawberry']
    ```

    > fruit.splice(2, 1)

05. Given these two objects: How could you add each to the others friends arrays?

    ```js
    let you = {
        name: "You",
        hair: true,
        friends: []
    }
    let them = {
        name: "Them",
        hair: false,
        friends: []
    }
    ```

    > you.friends.splice(0, 0, them) _OR_ you.friends.push(them)


06. Give an example of a JavaScript `Conditional`:

    > let x = 9
      let y= 20
      if (x > y){
        console.log(x);
      }
      else{
        console.log(y);
      }

07. What is the main difference between `parameters` and `arguments`?

    > Parameters are placeholders for arguments inside a function. They give room for the values (arguments) that you are going to pass through your function. 

08. Instead of writing everything to the console, what is a better way to debug your code?

    > You can test an debug your code in the Dev Tools in your browser. You can test color, alignment, or use the tools to find specific areas in your code that are throwing errors. They will also highlight the sections that aren't working and give a brief error message that you can use to debug your code. Additionally, you should build in tests in your code that can catch when something you write later breaks your code. This should be in addition to keeping the mindset of code small test small. Test all the time, basically!!

09. What is the difference between a `primitive` value and a `reference` value?

    > A primitive value is a value like a number, string, or boolean. A reference value is anything that isn't a primitive value, like an object or array. Reference values contain primitive values.

10. Demonstrate a loop that prints the numbers between -100 and 100?

    > for (let i = -100; i <= 100; i++) 
      {
        console.log(i)
      }
