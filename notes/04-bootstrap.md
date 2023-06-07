# Bootstrap

##SECTION - Getting Started

1. Include a bootstrap link reference in html head
    - This is on the bootstrap website and is linked with step 2.

2. link:bs5 in html head

3. Add header, main, and footer sections
    - Give these sections "container" classes.

4. Give applicable containers a new element and give them the "row" class.

5. Add whatever sections, divs, and p tags where needed. These will have "col" classes with the numbers that you would like.

6. Debugging is very useful. Add style:debug to html above the body in order to see where each section is. Don't forget to add the debug class to the body!



##SECTION - Facts

- BS starts with containers and there are grids with rows inside each container. The containers are all flexbox with flex-direction:row. The rows fit the width of the container, and there can be as many rows as needed. 
    - There are typically columns within the row, and each column can contain their own html.
    - There are 12 units of space within each row, and we control how the sizing works.

- BS makes the website styling much easier as a lot of it is automated for sizing and flexing. It's very customizable as a result.

- You can add break points which automatically change based on the screen size arguments that you provide.

- You cannot put columns in columns, rows in rows, etc.

- You do not need to make the columns add up to 12. Any extra space can be used in different justify-content classes, which can also be used for troubleshooting if your elements aren't moving the way that you want them to.

- Use the website for assistance on finding specific text/background/etc. colors. Copy and pasting is encouraged on this, for ease!

- _Global code snippets have been added to laptop vscode, so link: will provide useful code snippets. Check the slack page to put it on the desktop!_



##SECTION - Utility Classes





##SECTION - Syntax

**These are code snippets that you put in a class in the html sheet. You do not need to write them in the CSS sheet first!**

> col-1 (1 column)
> col-md-4 (on medium screen, provide 4 columns)
> justify-content-between|center|etc. (will automatically add this property to elements because it is a premade BS class.)
> d-flex (add display flex to columns or any other element that isn't automatically flexed.)
> m-NUMBER (adds a margin)
> mx-NUMBER (adds a margin only to the x-axis)
> my (margin on y-axis)
> m-start/s (margin only on start/left)
> me (margin only on end/right)
> bg (background, e.g. bg-primary changes the background color to a blue hue)
> text (text style, e.g. text-light changes the text color to a white hue)

> **container-fluid (will remove margins from the container so that it stretches edge-to-edge.)**