# Bootstrap

#TODO - Things to add, change, do.

- _Global code snippets have been added to laptop vscode, so link: will provide useful code snippets. Check the slack page to put it on the desktop!_

##SECTION - Getting Started

1. Include a bootstrap link reference in html head
    - This is on the bootstrap website and is linked with step 2.

2. link:bs5 in html head

3. Add header, main, and footer sections
    - Give these sections "container" classes.

4. Give applicable containers a new element and give them the "row" class.

5. Add whatever sections, divs, and p tags where needed. These will have "col" classes with the numbers that you would like.

6. Debugging is very useful. Add style:debug to html above the body in order to see where each section is. Don't forget to add the debug class to the body!
    - Take it off when your project is ready to grade.

7. Have fun coding! Check notes, references as needed.



##SECTION - Facts

- Use the Bootstrap website liberally for assistance! Website link: https://getbootstrap.com/

- BS starts with containers and there are grids with rows inside each container. The containers are all flexbox with flex-direction:row. The rows fit the width of the container, and there can be as many rows as needed. 
    - There are typically columns within the row, and each column can contain their own html.
    - There are 12 units of space within each row, and we control how the sizing works.

- BS makes the website styling much easier as a lot of it is automated for sizing and flexing. It's very customizable as a result.

- You can add break points which automatically change based on the screen size arguments that you provide. It will apply on the given class size and UP.

- You cannot put columns in columns, rows in rows, etc.

- You do not need to make the columns add up to 12. Any extra space can be used in different justify-content classes, which can also be used for troubleshooting if your elements aren't moving the way that you want them to.
    - You can also make the column size smaller to help with centering the content, instead of adding a bunch of padding to center something.

- Use the website for assistance on finding specific text/background/etc. colors. Copy and pasting is encouraged on this, for ease!

- Some BS properties have a similar name but different function. bg-primary is blue, where text-primary is white. Be carefuly about that!

- BS has higher specificity than CSS, so make sure your CSS stylesheet comes second to the BS stylesheet. This will help with specificity. If you want to override a BS property/code snippet, use the !important tag on your own code to guarantee that BS will be overwritten.

- If you add margins to your columns in the x-axis (you shouldn't), it may break your code if your columns add up to 12, or depending on their size and the margin size.

- Don't forget to use breakpoints to help change your style for mobile devices! They work similarly to media queries, but you add the class to the specific element so that it has the if statement contained. For example, col-md-6 will change the columns to 6 on screen sizes below medium size. Check the bootstrap website for specific screen size details.

- "Hero" section is the one where the mottos typically are that the user sees first.

- If you inspect a main page you can find the links used for assets, this will typically only be used on client projects or on CodeWorks assignments!

- It may be easier to set the default size of objects to the mobile size, and then create conditional properties as a screen size gets bigger.

- Even though columns should add up to 12, if you go over that number they should snap. So, you can have multiple elements in the row that will snap depending on mobile devices and other screens.

- You will only use align-items for flex boxes. Text-center may be preferred depending on the element.

- If you want icons or buttons to sit next to each other, put them in a flex container. **Don't forget about flex containers!**

- **To include images that are custom, give them their own CSS class instead of putting them in the html. You can also create them as backgrounds in this way with background-image. This will help it take up the entirety of the background that you want it to, to put text on top of.**
    -EXAMPLE:
    .hero-img{
        background-image: url(LINK);
        height: 30vh;
        background-size: fill;
        background-position: 10% 37%;
        background-repeat: norepeat;
    }

- To create a glassy, opaque color, use css.glass (Glassmorphism).
    - This will be used to create a CSS class selector.

- To make sure a text box stays a good height no matter the amount of text given, give it a min-height instead of a set height. This will allow the box to stay at a good size if the text is small, but then grow if there is more text.


#NOTE - Media Queries

- If you need your webpage to do something more specific than just changing column sizes, create a media query (media rules). We need to also provide a specific viewport for these rules. Good practice is copying the BS sizes for their breakpoints, as it will make the changes consistent throughout all devices and codes. 

- Media rules should be written on the bottom of the CSS doc. 

- EXAMPLE:
    @media (max-width: 768px #NOTE - max-width is preferred, as if you set it to just width then the rule will only work when the width is EXACTLY the px count){
        #NOTE - Any rules we add in the media rule, will occur when the screen is below this given size. Media rules are industry standards.
        #NOTE - In this example, we're changing borders that were originally on the left and right of an element to the top and bottom according to this rule.
        border-left: none;
        border-right: none;
        border-top: 3px solid black;
        border-bottom: 3px solid black;
    }

- If you want two different rules on a media query the syntax would be:
    - @media ((min-width: 500px) and (max-width: 768px))
    - The two rules are nested in the same parentheses, with each rule having their own parentheses.
    - You can use this syntax with OR as well.



##SECTION - Utility Classes

- Floating Navbar: **sticky-top**
    - The navbar (or whatever you apply sticky-top to) will stick to its direct parent, which is typically the top of the webpage.

- Image Blocks: **img-fluid**
    - The image will only be inside the given column that it is in. It will snap to the size of the column and stay on the page without bleeding over. Easier than resizing in CSS!
    - The image will not fill the column if it is smaller than it, but it will guarantee that it won't spill over.

- Buttons: **button** 
    - Will automatically add a button tag.
    - You can add icons into the text section of the buttons by placing them on the inside, like on a p tag. 
    - btn btn- adds styling to it depending on what you want. btn tells it to add button styling, btn- is what specific styling you want.
    - Hover interaction is added automatically. If you want the hover to look specific to what you want, you may need to add !important as explained above.

- Forms: _Still new to us! Use Bootstrap website and copy paste what you want for now._
    - If you want space between form submission sections, add some margins!

- Hyperlinks: "a" tags will add links to the text you put inside the tag.

- Order: **order-NUMBER**
    - Change the number to be the order which you want each element to be in within the parent element. This will make it so that they are in the order you desire, rather than in the order that you wrote the code in html.


##SECTION - Syntax

**These are code snippets that you put in a class in the html sheet. You do not need to write them in the CSS sheet first!**

> col-1 (1 column)
> col-md-4 (on medium screen, provide 4 columns)
> justify-content-between|center|etc. (will automatically add this property to elements because it is a premade BS class. align-items works similarly)
> d-flex (add display flex to columns or any other element that isn't automatically flexed.)
> m-NUMBER (adds a margin)
> mx-NUMBER (adds a margin only to the x-axis)
> my (margin on y-axis)
> m-start/s (margin only on start/left)
> me (margin only on end/right)
> bg (background, e.g. bg-primary changes the background color to a blue hue)
> text (text style, e.g. text-light changes the text color to a white hue)
> p-NUMBER (padding, MUST USE NUMBER BETWEEN 1 AND 5, has the same syntax as margins for x-axis|y-axis|etc.)
> pe (padding on end/right)
> fs-NUMBER (font size, MUST USE NUMBER BETWEEN 1 AND 5, similar in size to h tags in html, this can also be used on icons given in vscode - e.g., mdi)
> fw (font weight, e.g. fw-bold will make the font bold)
> d-none (no display, nothing is seen)
> .col12 (will automatically make a div with the given property that follows the .)
> rounded (will round edges of objects, won't make them circular though! If it isn't as round as you'd like, make your own CSS class.)
> .col6*2 (will automatically make the div with class as above, but will make as many as you are multiplying by.)
> order-NUMBER (will be in the given order from left to right ~ order-1 would be the first thing on the page read from left to right.)

> **container-fluid (will remove margins from the container so that it stretches edge-to-edge.)**

##SECTION - Figma

- Use Colormind to choose your color palette. Then, copy the hex values and put them in a square on the side. This is a an easy way to quickly use your color palette without flipping back and forth between pages.
    - Colormind also has advice on how to use colors (light, dark, accent, etc.). It's a good reference!

- You can give colors nicknames and quickly grab them in the hex code selector box instead of retyping the hex value.

- To put a new font into your webpage, go to Google Fonts. 
    - Copy the link tag and put it in the head.
    - Add the class of the font to the specific area that you want, as a css class that you make (such as .header-font, or you can use it as an element selector).

- You can use the Unsplash plug-in inside figma to pick your picture, rather than searching on the Unsplash website.

- Don't forget about hero sections! They will be underneath the header, before contact information and most links. It's the first thing a user will have their eye drawn to, and it will have the call to action on it.

- Images will often not fit the same way in actual code as it does in Figma. Make sure to use CSS classes to help with this.

- Work in "passes". Get the skeleton done first, then work on fonts, colors, pictures, etc.

- Use meettheipsums to generate differently-themed ipsums. Copy and paste the text into the area that you would like. Make sure there aren't swear words in the text, and pick ones that are generally professional. All projects that we make will be in our portfolio.

###NOTE - Figma Syntax

- Use CTRL+G to group items together. 

- To copy quickly use ALT and drag & drop.

