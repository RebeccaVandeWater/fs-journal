# Single Page Applications with Vue
01. What is the entrypoint of an application? #REVIEW - Is this correct?

  > The entrypoint is the URL provided in the page and in an API. For example, '/' in a plain Vue folder would open up just the Home page. Or, '/about' would open up the About page.

02. What is the difference between a vue `component` and `page`?

  > A component contains HTML, Javascript, and CSS that would apply to just one component of an application. A page contains only HTML so that 

03. What is ***Component-Based Architecture***?

  > Component-Based Architecture is a model where each component in an application that would have several functions and/or API's connected to them are encapsulated away from each other. This allows for more UI, but has the problem of becomming over-engineered and bloated. However, it is very popular because of its ease of use for both developers and users.

04. What are the three tags that make up a Vue component?

  > template - This is the HTML tag section.
  > script - This is the Javascript tag section.
  > style - This is the CSS tag section.

05. What are ***lifecycle hooks***? What are lifecycle hooks used for? #REVIEW - Add notes from lecture as applicable.

  > Lifecycle hooks are the commands used in the lifecycle of a component before, during, and after page load. The different kinds of hooks are creation, mounting, updating, and destruction hooks. All of these will effect your component throughout its use on a page.

06. Which component in Vue does the vue-router use to mount pages onto?

  > Vue still uses router.js to run pages like a controller normally would. It also has a createRouter and loadPage which both help to open the page that we have connected with a path in the router. You can make these objects which may have one path that then branches into children depending on the page. In the documentation example, you could have the parent path "/travel" that then can branch into children:[] that append onto the parent path and move to further pages.

07. What is the difference between the `AppState` and the state object within a component?

  > The AppState creates global variables that we can manipulate in different services. A state object is scoped exclusively to the vue component file it was made in.

08. What is the responsibility of `Services` in our Vue projects?

  > Services will manipulate AppState objects so that they are encapsulated away from the user.

09. What are ***props*** and how are they used? Provide an example

  > Props are variables that are passed down from a parent element into a child. They are placeholders for information that is specific to the type that they allow. When we create a model in Node, we use props to let the API know to expect a String, Boolean, Number, etc. In Vue, we use :binding to restrict the data type.

10. What is the Vue method used to create watchable objects such as `state` or `AppState`?

  > reactive() creates listeners and emitters to watchable objects. This takes out the need to add these ourselves with AppState.on() or AppState.emit().
