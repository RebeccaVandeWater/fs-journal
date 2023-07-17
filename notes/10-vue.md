# Vue

#SECTION - Getting Started
1. bcw create > vue-starter
2. Name the project, don't init the repo
3. cd into your project and code .
4. Spin up the project with run/debug on the client side (you will not have to spin up your client when you have changes, as well)

#STUB - Vue tour
- package.json installs all of the dependencies for the project, including vue, bootstrap, and axios.

- vite.config.js allows us to spin up our project and view it in development mode.

  - We also have app.vue files that the browser cannot read. Vite converts it so that it can read it on the development side, but doesn't make the website live for a user.

- index.html has almost no code in it. Additionally, it will not work without Javascript enabled.
  - In the main.js is some hookups that inject our code into the "app" div in the index.html. It takes the vue code and puts it there with a Create App import.

- env.js looks the same as it always has. 

- In app.vue
  - It contains html (template - like the body tag in a regular html file), javascript (script), and css (style) in the same file
    - You can add the scoped tag to the style if you would like to make sure that the styles in a file only affect the ones in that file. Otherwise, they are global by default.

- The components folder holds html for specific parts of your application, such as a navbar or card. Then, you can bring that component into other components or pages. This keeps the code encapsulated and organized.

- The Pages folder holds the "views" from the mvc pattern. For example, the about page or home page.

#SECTION - Using Javascript inside Vue
1. Making variables:
  - Inside the export default setup return
    cheese: 0
  - #REVIEW Anything that you want to return to the html MUST exist inside this return object. Anything put into setup is not accessible to the user, it would make the functions and variables private. The return is public.

2. To make the javascript appear inside the html, use double curly braces
  <p>Cheese: {{ cheese }}</p> #NOTE The double curlies act like string interpolation

3. To make a reactive function, like onclick:
  - Inside the tag in html:
    v-on:click="mineCheese()"

  - Inside the return:
    mineCheese(){
      cheese.value++
      logger.log('Cheese went up:', cheese) 
      #NOTE: This is a utility that puts timestamps on the console logs. Get used to using this INSTEAD of console.log, console.log will no longer be supported going forward as we move into the industry as it breaks quite a bit of code.
    }

    to make a variable reactive: let cheese = ref(0)

4. To use the AppState to save something:
- Inside the AppState:
  - The AppState has a reactive property inside it that makes all of the variables in it automatically reactive
  - Declare your instance in the AppState
    cheese: 0,

  - Inside the return, to bring in the variable from the AppState:
    cheese: computed(() => {return AppState.cheese})
    #NOTE this is an anonymous function that returns something from the AppState reactively. This is technically a getter. Computed is a function that takes in a function as its argument.
  
  - Remember that the controller should not be able to change data (the script inside the vue folder is technically the controller), so you need to write functions that manipulate data in the AppState in the service.
    - Make a service, and make sure it has imports in it (which are sometimes not compatible, and you might need to write them yourself)
    - In the service:
      mineCheese(){
        AppState.cheese++
      }

    - In the controller's return 
      cheeseService.minecheese()

#SECTION - Making a model with vue
- Make a class model like you normally would
  export class Upgrade{
    constructor(data){
      this.name = data.name
      this.quantity = 0
      this.multiplier = data.multiplier
      this.isTypeClick = data.isTypeClick
      this.price = data.price
    }
  }

- Build out your AppState instance
    upgrades: [
      new Upgrade({ name: 'pickaxe', price: 10, multiplier: 1, isTypeClick: true }),
      new Upgrade({ name: 'drill', price: 20, multiplier: 2, isTypeClick: true }),
      new Upgrade({ name: 'rover', price: 30, multiplier: 1, isTypeClick: false }),
      new Upgrade({ name: 'mousetronaut', price: 40, multiplier: 5, isTypeClick: false }),
    ]

- #TODO: You can check items in the AppState with the vue devtools! 

#SECTION - To return information from a model in the AppState
- You will likely need to put compute on the item to make sure that it reacts to the frontend changes
  upgrades: computed(() => AppState.upgrades)

- Don't forget to give it a place to go in the html template! 
  - To give an object's properties a place to go, where there are multiple objects:
    <div v-for="upgrade in upgrades" :key="upgrade.name" class="col-6"> 
    #NOTE This is a for loop inside vue that replaces a getter! The key is the unique property on each object that it wants to look at to take note of. The : binds the object's property to its key. Anything passed here is scoped to here as well. You can't use the upgrade inside a different html element

      <h2>{{ upgrade.name.toUppercase() }} || Multiplier: {{ upgrade.multiplier }}</h2> #NOTE We made this the name of one thing in the v-for above
      <h3>${{ upgrade.price }} </h3>
      <h3>Qty: {{upgrade.quantity}} </h3>
      <button class="btn btn-success"> </button>
    </div>

- A cool thing you can do is make another binding statement that will conditionally add css classes to items:
      <button class="btn" :class="{'btn-success': upgrade.isTypeClick, 'btn-info' : !upgrade.isTypeClick}"> </button>
      This will apply the btn-success color if isTypeClick is true, or btn-info if it is false. This is written like a turnary with true on the left and false on the right of the colon. Anything written inside the quotes is written as plain javascript when the colon precedes it. This is a great way to disable buttons on a condition!

      <button class="btn" :disabled="cheese < upgrade.price"> </button>

- Another way to write an onclick:
  <button class="btn" :disabled="cheese < upgrade.price" @click="buyUpgrade(upgrade.name)"> </button> #NOTE You can pass in the entire object as well. (upgrade)
  - In the function/controller:
    buyUpgrade(name){
      logger.log(upgrade)
      if(upgrade.price > AppState.cheese){
        Pop.error('Mine more cheese!')
        return
      }
      cheeseService.buyUpgrade(upgrade)
    }

    - In the service:
        buyUpgrade(upgrade){
          upgrade.quantity++
          AppState.cheese -= upgrade.price
          upgrade.price *= 2
        }

        mineCheese(){
          AppState.cheese++

          AppState.upgrades.forEach(u => {
            if(upgrade.isTypeClick){
              AppState.cheese += (upgrade.multiplier * upgrade.quantity)
            }
          })
        }

    - We can make a stat for this that is a computed multi-line function:
      clickPower: computed(() => {
        const clickUpgrades = AppState.upgrades.filter(u => u.isTypeClick)
        let total = 1
        clickUpgrades.forEach(u => total += (u.multiplier * u.quantity))
        return total #NOTE computed's always have to return a value
      })

    - 

- To prevent a default:
  @contextmenu.prevent="mineCheese()"
  The .prevent prevents the default. The @ is the v.directive, v.on will work the same way, but @ is faster.