# CSS

#SECTION - position, align, flex, justify

- position: absolute
    - allows you to move an element from its normal setting, so that it can be on top of a parent element. 
    - make sure the element is absolute to the column that it is in, not the entire page.
    - EXAMPLE:
        .buy-button{
            position: absolute; #NOTE - The position: absolute only works because the div that this buy-button's element is inside has had position-relative assigned to it.
            top: 85%;
            bottom: 43%;
        }

- position: relative
    - Makes the element a "relative" to the following elements. So, it can be the parent of a child element so that position: absolute doesn't make the child element move around an entire page.


- Everything is already position: static, which means that it has its own position. These change that to allow it to move on the page for overlapping with parent and child elements.

- Don't always use BS to help you move elements around. It may be more efficient to just write your own CSS class.

#NOTE: resizing images in CSS
.menu-img {
    height: 30vh;
    object-fit: cover;
}