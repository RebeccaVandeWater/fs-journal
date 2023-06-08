# Foundations of Web Development
01. In your own words, why do we use Git?
    > Git allows you to put your data in the cloud so that you or your team can use it later. This is useful when using different devices or working remotely. Your team also needs access to the code you are all working on, so that you can all use the most up-to-date version of the code without creating conflicting sections.

02. In the terminal, what is the command `mkdir` used for?
    > Make Directory

03. What is a ***pseudo-class*** and what are some of the most common ones you think you will use?
    > Pseudoclasses are arguments that target elements when they are under a specific condition. For example, .button may be its own class, while .button:hover targets that button when the user is hovering over it. I know I will use :hover quite often, but I haven't used a wide variety of pseudoclasses yet (or just haven't noticed closely when I have used them). I am interested to see which ones I will use and learn about!

04. What is ***specificity*** and how might you use it to your benefit?
    > Specificity is the order that your code is read and implemented. Code with a higher specificity score will be used over code that is lower. Classes are more specific than elements, so those properties will be implemented over element properties.

05. What problems do you think you could run into if you over-utilized the `!important` feature?
    > Everything will have the highest possible specificity and some rules will likely not be implemented the way that you want them to. Your code will very likely conflict with itself.

06. What are the three components that makeup a `CSS` rule? <br> Example:

    ```css
        h1 {
            color: rgba(255, 210, 33, .75);
        }
    ```

    > Selector, property, and value. The selector is what element we want to style, the property is the style we want to apply, and the value is the specific amount of the style such as hexcode for color, pixels for height, etc.

07. How do you think good design influences people when visiting a website, and what sorts of things could you convey through design alone?
    > Good design on websites quickly and easily conveys essential information to users. If it is nice to look at, and helps draw the user's eye to important information like what the company does, they can decide whether they will be able to use the company for what they need. Things conveyed through design are the purpose of the company, important information like calendars and schedules, and how to contact the company.

08. What is the purpose of ***wireframing***?
    > Wireframing shows clients and stakeholders the concept of a website, either in a very basic form like a sketch, or in a highly detailed form like a Figma page.

09. Do you think wireframes are worth the time, energy, and effort that they require? Why or Why not?
    > I think that wireframes are extremely helpful! They convey information about the concept of a website that can be misunderstood or poorly conveyed in just verbal explanations. Additionally, they create a great reference for team collaboration on what should or should not be on the website.

10. Define the display `:flex property:`
    > Flex moves elements in a section around each other relative to each other and the box that they are in.

11. What `CSS` properties affect the size of a box model?
    > Height and width.
