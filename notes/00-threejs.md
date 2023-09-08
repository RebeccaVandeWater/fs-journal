# three.js & UI/IX

#SECTION - Styling and Layout
- Sidescroll > Occurs when you have more than one container-fluid class, in addition to breaking the bootstrap grid. Container fluid should be the first div inside a vue template.
  - If really struggling with side-scroll, you can put inline styling: overflow:hidden; in order to force it to stop. Not recommended in all cases, but can fix it.

#SECTION - Key Animations/Subtle Animations
  #STUB - Fade in > create a custom CSS class
  - .animate{
      animation: (name) fadeIn (duration) 2s (transition) ease-in-out (duration until animation occurs) 2s (how many times it occurs, in this case once) forwards; 
    }
  - ease in starts slow, ends fast
  - ease out starts fast, ends slow
  - ease-in-out combines the two
  - infinite is continuous animation

  - @keyframes fadeIn {
      0% {
        opacity: 0;
      } (what will it do when it starts)
      100% {
        opacity: 1;
      } (What it will do when it finishes. It will stay like this after it reaches this percentage of completion)
    }
  > This targets the animation that you set when the page loads and the appropriate duration occurs. Keyframes will override css classes that you define in the specific element.

  - pointer events > What happens when you hold your mouse over an element

  #STUB - Slide in > Make sure to define the custom CSS class
  - @keyframes slideIn {
      0%{
        transform: translateX(-100%); > Takes it completely off the page to the right, 100% will take it completely off the page to the left.
      }
      100%{
        transform: translateX(0%); > Moves the element over to its original position
      }
    }

  - Use the tip above to fix any sidescroll that might occur because of this animation. You can also start the animation closer to its end point, rather than off the page.

  - Animations will preferably go on a row, not a column

  #STUB - ::before or ::after
  > in this pseudo class, you add:
    content: '', > This instantiates your pseudo class, you'll typically not put anything inside of the string.
    position: absolute;
    top: 2.5em;
    right: 0%;
    left: 0%;
    width: 100%; > Mirrors the actual element, this is the width of that element
    height: 100%; > Like with the width, this inherits the height of the element
    transition: transform .5s ease-in-out > How long will it take for this animation to complete?
    transform: perspective(1em) rotateX(40deg) scale(1, .35)> squishes along the x-axis; perspective should come first because it will be following the rules of the other defining properties that follow it; scale has an x and y value so that it spreads and then shrinks it
    filter: blur(1em);

  #REVIEW - animatebackgrounds.me > not keyframes, simple animations on the backgrounds that is free!

  #STUB - Image Panning
  - In your keyframes query, it will be better to create more than two keys, such as 0%, 25%, 50% ... 100%. 
  - Target the background position at different positions in order to pan over an infinite animation
  - Better to make the animation take 60 - 120s or more so that it pans nicely without being distracting

#SECTION - Color Psychology
- Red: Powerful accent color, but can be overwhelming > Great to represent power or passion. In a tech website, red and black are used to represent risk and power. They are someone who takes risks and has a powerful design

- Blue: Represents trust

- Yellow: Can make people feel insecurity if used too much, but if used as an accent can represent urgency. When used with blue it feels like you need to "buy now"

- Orange: Good blend between red and yellow; playfulness and urgency > pale yellow and light blue work very well together

- Rainbow: Not used often, usually just in logo. If used overboard will give off a child-like feeling, which can be good or bad. Makes people feel positivity, creativity, and joy

- 60/30/10: 60% dominant color, 30% secondary/supporting color, 10% accent color (text shadow/box shadow)

#SECTION - Tips & Tricks

- email.js > Have people email you with little setup on your end

