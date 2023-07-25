# Managing the Fullstack Application

1. Describe the two ways to bind Data in Vue?

  > You can use one way binding with something like :key. The colon indicates that we are binding the class onto something that we provide it with after the equal sign. We can also use v-model to create two way binding, which is described below in question 5.

2. The `SPA` acronym stands for what?

  > S: Single
  > P: Page
  > A: Application

3. What are some of the advantages/uses of a `SPA` over a traditional one?

  > In traditional applications, we have the HMTL file and Javascript file separate. This results in more time being needed to load the application because the HTML will be rendering while the Javascript is downloading. SPA allows the page to render while the JS is downloading, resulting in a faster user experience in most cases.

4. What does the `onMounted` method in Vue do?

  > onMounted is a lifecycle hook in Vue. It runs code when the page is initially mounted into the router-view.

5. What is the `v-model` attribute in Vue for, and when might you use it?

  > The v-model attribute creates properties on a reference object so that we can build out that object as a user interacts with it. The most common way that we have used it is with building out an object from a user interacting with a form.

6. What is the package.json file used for?

  > package.json downloads the different packages required for node and vue to function. This also how we add additional helpful tools like MDI Icons or Google Fonts.

7. Which Vue attributes(directives) could you use to conditionally render elements on a page?

  > v-if: This does not render an element unless it meets the conditions in the v-if.
  > v-show: This renders the element, but hides it with a display-none unless it meets the conditions of the v-show.

8. What is the purpose of the `key` attribute when using `v-for` on an element?

  > The key is how the for loop in the v-for keeps track of which items it iterates through. The key should be bound to something unique so that the items are iterated through correctly.

9. What is the `<slot>` element and what is it used for?

  > The slot element allows us to insert information into component areas that we save with the slot. It allows us to reuse components so that we don't need to build out as many components. For example, in class we use slots to slot in different form components into the same Modal component.
