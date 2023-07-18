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

- To prevent a default:
  @contextmenu.prevent="mineCheese()"
  The .prevent prevents the default. The @ is the v.directive, v.on will work the same way, but @ is faster.

#SECTION - Building models with API's

- Make sure to read the documentation on an API to see what is required in the URL to pull off an object. Some API's require a query, others don't. The Giphy API requires a key, for example.

- Create an axios instance to talk to the API inside the AxiosService. Look at the const api = Axios.create({}) as an example of how to do this. Timeouts are always recommended as they will be needed if they are connected to the Auth middleware.
  - You can put the API key automatically into each request by adding a key/value pair inside a params. You can also add a filter here.
    params{
      api_key: "<API KEY>",
      include_adult: false,
      certification_country: 'US',
      'certification.gte': 'G', #NOTE this is made into a string due to the dot notatation of this parameter
      'certification-lte': 'PG-13'
    }

- Go to your function/controller, make sure that you have the template, script, and style tags.

#STUB - Required functions to get started:

1. In the componenet, outside of the return, set up:
  onMounted(()=>{ #NOTE what will the component do when the page first loads? If connected to a database, this would be a great time to get all the things from that DB.
    logger.log("Home Page Mounted")

    async function getMovies(){
      try{
        await 
      } catch(error){
        Pop.error(error, 'Getting Movies') #NOTE The string is a good notification of what went wrong doing what.
      }
    }
  })

  unMounted(() => {
    logger.log("Home Page Unmounted")
  })

  - In the service: #NOTE Make sure that this is imported into the component.
    class MoviesService{

      async getMovies(){
        const res = await movieApi.get('/discover/movie')

        logger.log('Got Movies:', res.data)
      }
    }

    export const moviesService = new MoviesService

    - Put the function inside the onMounted, not the return. This allows the page to grab the data on load:
    onMounted(()=>{ 
    logger.log("Home Page Mounted")
    getMovies()
    })

2. Make the model for the component:
  export class Movie {
    constructor(data){
      this.id = data.id
      this.originalLanguage = data.original_language
      this.originalTitle = data.original_title
      this.title = data.title
      this.overview = data.overview
      this.popularity = data.popularity
      this.releaseDate = data.release_data
      this.poster = `<URL>/${data.poster_path}`
      this.backdrop = `<URL>/${data.backdrop_path}`
    }
  }

3. Now that the data is in the console and we have a model, we should store the information in the AppState
  - In the AppState:
    movies = []

4. Map the new data in the service, and save it in the AppState
  async getMovies(){
        const res = await movieApi.get('/discover/movie')

        logger.log('Got Movies:', res.data)

        const movies = res.data.results.map(moviePojo => new Movie(moviePojo))

        AppState.movies = movies
      }

5. Double check that you can see the data by printing the data into a string with your html template. You can take the HTML away once you have confirmed that the data is being brought in correctly:

  - In the template:
  <div>{{ movies }}</div>

  - In the return:
  movies: computed(() => AppState.movies) #NOTE Don't forget to use computed in order to make sure the data is "reactive", i.e., has a premade listener on it.

6. Make a v-for to generate HTML for the items that you have pulled down:
  EXAMPLE:
  <h2 v-for="movie in movies" :key="movie.id">{{movie.title}}</h2>

  #REVIEW: Remember that {{}} are used for text content from a model, whereas :binding is used if you would like the value of something in the html (like the img url) to be set to the value of the text of the model.
  EXAMPLE:
  <img :src="movie.poster" :alt="movie.title">

#STUB - To use multiple pages to pull down A LOT more content from an API

1. Store the page number and total pages in the AppState with a new object
  page: 0,
  totalPages: 0

2. In the service: 
  async getMovies(){
    const res = await movieApi.get('/discover/movie')

    logger.log('Got Movies:', res.data)

    const movies = res.data.results.map(moviePojo => new Movie(moviePojo))

    AppState.movies = movies

    **AppState.page = res.data.page**

    **AppState.totalPages = res.data.total_pages**
  }

3. In the return:
  page: computed(() => AppState.pages)

  totalPages: computed(() => AppState.totalPages)

4. In the template:
  <h2>Page {{page}} of {{totalPages}}</h2>

5. Set up some buttons that move to the next page in the API:
  1. Template:
    <div class="d-flex justify-content-between">
    <button btn btn-primary @click="getPreviousPageOfMovies()">Previous Page</button>
    <button btn btn-primary @click="getNextPageOfMovies()">Next Page</button>
    </div>

  2. In the return (because it is public):
    async getNextPageOfMovies(){
      try{
        async moviesService.getNextPageOfMovies()
      } catch(error){
        Pop.error(error)
      }
    }

  3. In the service:
    async getNextPageOfMovies(){
      const res = await movieApi.get(`discover/movie/?page=${AppState.page + 1}`)

      logger.log('Got Next Page of Movies', res.data)

      #NOTE: While this is a lot of code, this is a great place to start before refactoring our code.
      const movies = res.data.results.map(moviePojo => new Movie(moviePojo)) 

      AppState.movies = movies

      AppState.page = res.data.page

      AppState.totalPages = res.data.total_pages
    }

    #STUB Let's refactor!

    -In the template:
    <div class="d-flex justify-content-between">
    <button :disabled="page == 1" btn btn-primary @click="getNewPageOfMovies(page - 1)">Previous Page</button>
    <button :disabled="page == totalPages" btn btn-primary @click="getNewPageOfMovies(page + 1)">Next Page</button>
    </div>

    -In the return:
    async getNewPageOfMovies(pageNumber){
      try{
        await moviesService.getNewPageOfMovies(pageNumber)
      } catch(error){
        Pop.error(error)
      }
    }

    - In the service:
    async getNewPageOfMovies(pageNumber){
      const res = await movieApi.get(`discover/movie/?page=${pageNumber}`)

      logger.log('Got Next Page of Movies', res.data)

      const movies = res.data.results.map(moviePojo => new Movie(moviePojo)) 

      AppState.movies = movies

      AppState.page = res.data.page

      AppState.totalPages = res.data.total_pages
    }

#SECTION - Abstracting out your code to different components
- Whatever code you made in the template, the script, and the style will have to be moved. Make sure that you grab all sections that are related to each other to move in the template.
  - #REVIEW The computed properties ONLY exists on the parent elements, the props ONLY exist on the child elements.
  - You may choose to keep a v-for in a div in the overhead page, so that you can generate that code depending on the number of things in an array. If you do this, you need to set up a prop to pass the data from the parent component to the child component:
    - Above the setup:
      props:{
        movieProp:{
          type: Movie, #NOTE This is from a previously made model
          required: true
        }
      },

    - In the Template in the parent element:
    <MovieCard :movieProp="movie"
    #NOTE Every time you draw the Moviecard, grab the movieProp and grab anything that has the name movie attached to it in that Type.

    - In the Template in the child element:
      <img :src="movieProp.poster" :alt="movieProp.title" class="img-fluid"></img>
      <h3>{{movieProp.title}}</h3>

#SECTION - Making another page

1. In the template, include a router link
  <router-link :to={name: 'Movie'}> #NOTE The to should match the route in your router
  #NOTE Asks what page we want to grab from our router view. They can break Vue very easily, though!! Make sure it has a :to on it to help with that.
  #NOTE In this case, the router-link exists on an object on a child object
    <img :src="movieProp.poster" :alt="movieProp.title" class="img-fluid"></img>
    <h3>{{movieProp.title}}</h3>
  </router-link> 

2. Make sure that you have a view page for the router link to go.
  - In the pages, write a new page.
    MovieDetailsPage.vue
    
    use vt to use the vue template stub

3. Create a new route object in the router

4. If you're passing in data to make a new page from an object, you'll have to pass in its ID into the URL.
  - In the router:
    path: '/movie/movieId',
    name: 'Movie',
    component: loadpage:('MovieDetailsPage')

  - In the :to #NOTE this router link is in a child page, hence why it's talking to the movie prop.
    :to="{name: 'Movie', params: {movieId: movieProp.id} }"

5. Make an onMounted and getById on the new page:

  const route = useRoute() #NOTE Use the route of the thing I am currently on

  async function getMovieById(){
    try{
      <!-- logger.log("Here is the route parameter Id", route.params.movieId) #NOTE always log the res to see what the path of the thing is that you want to grab -->
      const movieId = route.params.movieId
      await moviesService.getMovieById(movieId)
    } catch(error){
      Pop.error(error)
    }
  }

  onMounted(() => {
    getMovieById()
  })

  - In the service:
  async getMovieById(movieId){
    const res = await movieApi.get(`movie/${movieId}`)

    logger.log('Got movie by Id', res.data)
  }

6. Make a place to store this data in the AppState, then save it.
  - In the AppState:
  activeMovie: null

  - In the Service:
  async getMovieById(movieId){
    const res = await movieApi.get(`movie/${movieId}`)

    logger.log('Got movie by Id', res.data)

    **const movie = new Movie(res.data)**

    **AppState.activeMovie = movie**
  }

7. Make your page info:
  - In the return:
  movie: computed(() => AppState.activeMovie)

  - In the template:
  <div v-if="movie"> #NOTE This will notify the HTML to not load until there is a movie. You can use this INSTEAD of an elvis operator (below)
    <h3>
    {{movie?.title}} 
    
    #NOTE You can use an elvis operator to make sure that the thing exists before drilling into it. HTML will load before the function, so it will be a little bit ahead of the get function. We want to make sure that the elvis operator is there to wait until the function is done and then to go get the thing that triggered a listener.
    </h3>
  </div>